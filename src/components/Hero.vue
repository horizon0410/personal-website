<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const roles = ['Vue3 开发学习者', '前端工程化探索者', '个人项目开发者']
const displayed = ref('')
let roleIdx = 0, charIdx = 0, deleting = false, timer = null

function tick() {
  const cur = roles[roleIdx]
  if (!deleting) {
    displayed.value = cur.slice(0, ++charIdx)
    if (charIdx === cur.length) { deleting = true; timer = setTimeout(tick, 1800); return }
  } else {
    displayed.value = cur.slice(0, --charIdx)
    if (charIdx === 0) { deleting = false; roleIdx = (roleIdx + 1) % roles.length }
  }
  timer = setTimeout(tick, deleting ? 60 : 100)
}

const canvas = ref(null)
let raf = null, pts = []

function initCanvas() {
  const c = canvas.value
  c.width = c.offsetWidth; c.height = c.offsetHeight
  pts = Array.from({ length: 55 }, () => ({
    x: Math.random() * c.width, y: Math.random() * c.height,
    r: Math.random() * 2 + 1,
    dx: (Math.random() - 0.5) * 0.6, dy: (Math.random() - 0.5) * 0.6,
  }))
}

function drawCanvas() {
  const c = canvas.value, ctx = c.getContext('2d')
  ctx.clearRect(0, 0, c.width, c.height)
  for (const p of pts) {
    ctx.beginPath(); ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2)
    ctx.fillStyle = 'rgba(66,184,131,0.4)'; ctx.fill()
    p.x += p.dx; p.y += p.dy
    if (p.x < 0 || p.x > c.width) p.dx *= -1
    if (p.y < 0 || p.y > c.height) p.dy *= -1
  }
  for (let i = 0; i < pts.length; i++)
    for (let j = i + 1; j < pts.length; j++) {
      const dx = pts[i].x - pts[j].x, dy = pts[i].y - pts[j].y
      const d = Math.sqrt(dx * dx + dy * dy)
      if (d < 100) {
        ctx.beginPath(); ctx.moveTo(pts[i].x, pts[i].y); ctx.lineTo(pts[j].x, pts[j].y)
        ctx.strokeStyle = `rgba(66,184,131,${0.12 * (1 - d / 100)})`
        ctx.lineWidth = 0.5; ctx.stroke()
      }
    }
  raf = requestAnimationFrame(drawCanvas)
}

const showQR = ref(false)

onMounted(() => {
  tick(); initCanvas(); drawCanvas()
  window.addEventListener('resize', initCanvas)
})
onUnmounted(() => {
  clearTimeout(timer); cancelAnimationFrame(raf)
  window.removeEventListener('resize', initCanvas)
})
</script>

<template>
  <section class="hero">
    <canvas ref="canvas" class="particles" />

    <div class="hero-content">
      <div class="hero-text">
        <h1>你好，我是冯证杨</h1>
        <h2 class="typewriter">{{ displayed }}<span class="cursor">|</span></h2>
        <p>正在学习 Vue3、Git、前端工程化与项目部署，目前努力开发个人博客系统。</p>

        <div class="buttons">
          <a href="#projects"><button class="btn-primary">查看项目</button></a>
          <a href="https://github.com/horizon0410" target="_blank">
            <button class="btn-outline">
              <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12 0C5.37 0 0 5.37 0 12c0 5.3 3.44 9.8 8.2 11.38.6.1.82-.26.82-.58v-2.04c-3.34.72-4.04-1.61-4.04-1.61-.54-1.38-1.33-1.75-1.33-1.75-1.09-.74.08-.73.08-.73 1.2.08 1.84 1.24 1.84 1.24 1.07 1.83 2.8 1.3 3.49 1 .1-.78.42-1.3.76-1.6-2.67-.3-5.47-1.33-5.47-5.93 0-1.31.47-2.38 1.24-3.22-.13-.3-.54-1.52.12-3.18 0 0 1.01-.32 3.3 1.23a11.5 11.5 0 013-.4c1.02 0 2.04.13 3 .4 2.28-1.55 3.29-1.23 3.29-1.23.66 1.66.25 2.88.12 3.18.77.84 1.24 1.91 1.24 3.22 0 4.61-2.81 5.63-5.48 5.92.43.37.81 1.1.81 2.22v3.29c0 .32.22.69.83.57C20.57 21.8 24 17.3 24 12c0-6.63-5.37-12-12-12z"/>
              </svg>
              GitHub
            </button>
          </a>
          <a href="/resume.pdf" download>
            <button class="btn-outline">↓ 下载简历</button>
          </a>
          <div class="wechat-wrap" @mouseenter="showQR = true" @mouseleave="showQR = false">
            <button class="btn-outline">微信</button>
            <Transition name="qr-pop">
              <div class="qr-popup" v-if="showQR">
                <img src="/wechat-qr.png" alt="微信二维码" />
                <span>扫码添加微信</span>
              </div>
            </Transition>
          </div>
        </div>
      </div>

      <div class="hero-avatar">
        <img src="/avatar.jpg" alt="头像" @error="e => e.target.style.display='none'" />
        <span class="avatar-fallback">FZY</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  height: 100vh;
  display: flex;
  align-items: center;
  padding: 60px 10% 0;
  background: linear-gradient(135deg, #f5f7fa 0%, #e8f4ff 100%);
  overflow: hidden;
}

.particles {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.hero-content {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  gap: 40px;
}

.hero-text {
  flex: 1;
  max-width: 600px;
}

.hero-text h1 {
  font-size: clamp(28px, 4vw, 48px);
  margin: 0 0 20px 0;
}

.hero-text h2 {
  font-size: clamp(18px, 2.5vw, 28px);
  color: #42b883;
  margin: 0 0 20px 0;
}

.hero-text p {
  line-height: 1.8;
  color: #555;
  margin: 0;
}

.buttons {
  margin-top: 30px;
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  align-items: center;
}

.buttons a { text-decoration: none; }

.btn-primary {
  padding: 12px 24px;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 15px;
  transition: transform 0.2s, background 0.2s;
}
.btn-primary:hover { background: #33a06f; transform: translateY(-3px); }

.btn-outline {
  padding: 11px 20px;
  background: white;
  color: #333;
  border: 1px solid #ddd;
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  display: flex;
  align-items: center;
  gap: 6px;
  transition: transform 0.2s, box-shadow 0.2s;
}
.btn-outline:hover { transform: translateY(-3px); box-shadow: 0 4px 12px rgba(0,0,0,0.1); }

.wechat-wrap {
  position: relative;
}

.qr-popup {
  position: absolute;
  bottom: calc(100% + 12px);
  left: 50%;
  transform: translateX(-50%);
  background: white;
  border-radius: 12px;
  padding: 16px;
  box-shadow: 0 8px 30px rgba(0,0,0,0.15);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  white-space: nowrap;
  z-index: 100;
}

.qr-popup img {
  width: 140px;
  height: 140px;
  object-fit: contain;
  border-radius: 4px;
}

.qr-popup span {
  font-size: 12px;
  color: #888;
}

.qr-pop-enter-active, .qr-pop-leave-active { transition: opacity 0.2s, transform 0.2s; }
.qr-pop-enter-from, .qr-pop-leave-to { opacity: 0; transform: translateX(-50%) translateY(6px); }

.hero-avatar {
  position: relative;
  width: clamp(120px, 18vw, 220px);
  height: clamp(120px, 18vw, 220px);
  border-radius: 50%;
  background: #42b883;
  box-shadow: 0 10px 30px rgba(66,184,131,.3);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  overflow: hidden;
  animation: float 3s ease-in-out infinite;
}

.hero-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
}

.avatar-fallback {
  position: absolute;
  color: white;
  font-size: clamp(24px, 5vw, 48px);
  font-weight: bold;
}

.hero-avatar img:not([style*="display: none"]) + .avatar-fallback { display: none; }

.typewriter { min-height: 1.4em; }
.cursor {
  display: inline-block;
  animation: blink 0.8s step-end infinite;
  color: #42b883;
}
@keyframes blink { 50% { opacity: 0; } }

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-12px); }
}

@media (max-width: 768px) {
  .hero { padding: 80px 6% 40px; }
  .hero-content { flex-direction: column-reverse; text-align: center; }
  .buttons { justify-content: center; }
}
</style>