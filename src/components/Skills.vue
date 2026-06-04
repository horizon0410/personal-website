<script setup>
import { ref, computed, onMounted } from 'vue'

const skillGroups = {
  computer: [
    { name: 'Python',  level: 4 },
    { name: 'Java',    level: 3 },
    { name: 'Vue3',    level: 3 },
    { name: 'Git',     level: 4 },
    { name: 'MySQL',   level: 3 },
  ],
  modeling: [
    { name: 'SolidWorks', level: 4 },
    { name: 'ZBrush',     level: 3 },
    { name: '3ds Max',    level: 3 },
    { name: 'Blender',    level: 2 },
  ],
  design: [
    { name: 'Photoshop', level: 3 },
    { name: 'Premiere',  level: 3 },
  ],
}

const tabs = [
  { key: 'computer', label: '计算机开发' },
  { key: 'modeling', label: '三维建模' },
  { key: 'design',   label: '视觉设计' },
]

const levelMap = { 4: 80, 3: 60, 2: 40, 1: 20 }

const active = ref('computer')
const visible = ref(true)
const animating = ref(false)

const skills = computed(() => skillGroups[active.value])

function switchTab(key) {
  if (key === active.value || animating.value) return
  animating.value = true
  visible.value = false
  setTimeout(() => {
    active.value = key
    visible.value = true
    animating.value = false
  }, 220)
}

// 进度条入场动画：切换后依次延迟填充
const barWidths = ref([])

function fillBars() {
  barWidths.value = skills.value.map(() => 0)
  skills.value.forEach((s, i) => {
    setTimeout(() => {
      barWidths.value[i] = levelMap[s.level]
    }, 80 + i * 80)
  })
}

import { watch } from 'vue'
watch(active, () => { setTimeout(fillBars, 240) }, { immediate: false })
onMounted(fillBars)
</script>

<template>
  <section id="skills" class="skills">
    <h2 class="section-title">技能栈</h2>

    <!-- Tab 切换 -->
    <div class="tabs">
      <button
        v-for="tab in tabs"
        :key="tab.key"
        class="tab-btn"
        :class="{ active: active === tab.key }"
        @click="switchTab(tab.key)"
      >
        {{ tab.label }}
      </button>
    </div>

    <!-- 技能列表 -->
    <Transition name="fade-slide">
      <div class="skill-list" v-if="visible" :key="active">
        <div
          class="skill-card"
          v-for="(skill, i) in skills"
          :key="skill.name"
          :style="{ animationDelay: `${i * 60}ms` }"
        >
          <div class="skill-header">
            <span class="skill-name">{{ skill.name }}</span>
            <span class="skill-pct">{{ levelMap[skill.level] }}%</span>
          </div>
          <div class="bar-track">
            <div
              class="bar-fill"
              :style="{ width: (barWidths[i] ?? 0) + '%' }"
            />
          </div>
        </div>
      </div>
    </Transition>
  </section>
</template>

<style scoped>
.skills {
  padding: 90px 10%;
  background: linear-gradient(160deg, #f0f4f8 0%, #e8f4ff 100%);
  min-height: 60vh;
  transition: background 0.3s ease;
}

:global(.dark) .skills {
  background: linear-gradient(160deg, #16213e 0%, #1a1a2e 100%);
}

.section-title {
  font-size: clamp(24px, 3vw, 36px);
  margin: 0 0 40px;
  color: #1a1a2e;
  letter-spacing: 0.02em;
  transition: color 0.3s ease;
}

:global(.dark) .section-title {
  color: #fff;
}

/* ── Tabs ── */
.tabs {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
  margin-bottom: 40px;
}

.tab-btn {
  padding: 10px 24px;
  border-radius: 999px;
  border: 2px solid transparent;
  background: rgba(255,255,255,0.6);
  backdrop-filter: blur(8px);
  color: #555;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.25s ease;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}

:global(.dark) .tab-btn {
  background: rgba(255,255,255,0.08);
  color: #bbb;
  box-shadow: 0 2px 8px rgba(0,0,0,0.3);
}

.tab-btn:hover {
  border-color: #42b883;
  color: #42b883;
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(66,184,131,0.18);
}

:global(.dark) .tab-btn:hover {
  border-color: #64d8a8;
  color: #64d8a8;
  box-shadow: 0 6px 16px rgba(100,216,168,0.25);
}

.tab-btn.active {
  background: #42b883;
  color: white;
  border-color: #42b883;
  box-shadow: 0 6px 20px rgba(66,184,131,0.35);
}

:global(.dark) .tab-btn.active {
  background: #64d8a8;
  color: #1a1a2e;
  border-color: #64d8a8;
}

/* ── Skill list ── */
.skill-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}

/* ── Skill card ── */
.skill-card {
  background: rgba(255,255,255,0.55);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  border: 1px solid rgba(255,255,255,0.75);
  border-radius: 16px;
  padding: 22px 26px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.07);
  transition: transform 0.25s ease, box-shadow 0.25s ease, background 0.3s ease, border-color 0.3s ease;
  animation: card-in 0.35s ease both;
}

:global(.dark) .skill-card {
  background: rgba(37,37,65,0.6);
  border-color: rgba(255,255,255,0.1);
  box-shadow: 0 4px 16px rgba(0,0,0,0.3);
}

.skill-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 32px rgba(66,184,131,0.18);
}

:global(.dark) .skill-card:hover {
  box-shadow: 0 12px 32px rgba(100,216,168,0.25);
}

@keyframes card-in {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* ── Bar ── */
.skill-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
}

.skill-name {
  font-size: 15px;
  font-weight: 600;
  color: #222;
  transition: color 0.3s ease;
}

:global(.dark) .skill-name {
  color: #e0e0e0;
}

.skill-pct {
  font-size: 13px;
  color: #42b883;
  font-weight: 600;
  transition: color 0.3s ease;
}

:global(.dark) .skill-pct {
  color: #64d8a8;
}

.bar-track {
  height: 8px;
  border-radius: 999px;
  background: rgba(0,0,0,0.08);
  overflow: hidden;
  transition: background 0.3s ease;
}

:global(.dark) .bar-track {
  background: rgba(255,255,255,0.1);
}

.bar-fill {
  height: 100%;
  border-radius: 999px;
  background: linear-gradient(90deg, #42b883, #64d8a8);
  transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 0 8px rgba(66,184,131,0.4);
}

/* ── Transition ── */
.fade-slide-enter-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}
.fade-slide-leave-active {
  transition: opacity 0.2s ease, transform 0.2s ease;
  position: absolute;
  width: 100%;
}
.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(12px);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

/* ── Responsive ── */
@media (max-width: 768px) {
  .skills { padding: 70px 6%; }
  .skill-list { grid-template-columns: 1fr; }
}
</style>
