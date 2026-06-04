<script setup>
const timeline = [
  {
    year: '2024',
    title: '空气质量预测与数学建模项目',
    desc: '基于机器学习算法完成空气质量预测系统，参与数学建模竞赛',
  },
  {
    year: '2025',
    title: '学习 Git、Vue3 与前端开发',
    desc: '系统学习现代前端技术栈，掌握版本控制与工程化开发',
  },
  {
    year: '2026',
    title: '参与社区数字化治理平台开发',
    desc: '实习于中国电信中山分公司，参与社区治理信息化项目',
  },
]

const stats = [
  { label: '项目经验', value: '3+' },
  { label: '技术栈',   value: '10+' },
  { label: '持续学习中', value: '∞' },
]
</script>

<template>
  <section id="about" class="about">
    <h2 class="section-title">关于我</h2>

    <!-- 个人简介卡片 -->
    <div class="intro-card">
      <p>
        我是一名刚毕业于<strong>韩山师范学院</strong>的应届生，目前实习于<strong>中国电信中山分公司</strong>。
      </p>
      <p>
        我希望通过持续学习，逐步掌握技术，通过大模型提升效率，最终能独立完成项目。
      </p>
    </div>

    <!-- 时间轴 -->
    <div class="timeline-wrapper">
      <h3 class="subsection-title">成长历程</h3>
      <div class="timeline">
        <div
          class="timeline-item"
          v-for="(item, i) in timeline"
          :key="i"
        >
          <div class="timeline-marker">
            <div class="dot"></div>
          </div>
          <div class="timeline-content">
            <span class="year">{{ item.year }}</span>
            <h4>{{ item.title }}</h4>
            <p>{{ item.desc }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- 统计卡片 -->
    <div class="stats">
      <div
        class="stat-card"
        v-for="(stat, i) in stats"
        :key="i"
      >
        <div class="stat-value">{{ stat.value }}</div>
        <div class="stat-label">{{ stat.label }}</div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  padding: 90px 10%;
  background: white;
  transition: background 0.3s ease;
}

:global(.dark) .about {
  background: #1a1a2e;
}

.section-title {
  font-size: clamp(26px, 3vw, 36px);
  margin: 0 0 40px;
  color: #1a1a2e;
  transition: color 0.3s ease;
}

:global(.dark) .section-title {
  color: #fff;
}

/* ── 个人简介卡片 ── */
.intro-card {
  background: linear-gradient(135deg, #f7f9fc 0%, #eef5ff 100%);
  border-radius: 16px;
  padding: 32px 40px;
  margin-bottom: 60px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
  border: 1px solid rgba(66,184,131,0.1);
  transition: transform 0.25s ease, box-shadow 0.25s ease, background 0.3s ease, border-color 0.3s ease;
}

:global(.dark) .intro-card {
  background: linear-gradient(135deg, #252541 0%, #2a2a42 100%);
  border-color: rgba(100,216,168,0.15);
  box-shadow: 0 4px 20px rgba(0,0,0,0.3);
}

.intro-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 36px rgba(66,184,131,0.12);
}

:global(.dark) .intro-card:hover {
  box-shadow: 0 12px 36px rgba(100,216,168,0.15);
}

.intro-card p {
  line-height: 1.9;
  color: #444;
  margin: 0 0 14px;
  font-size: 15px;
  transition: color 0.3s ease;
}

:global(.dark) .intro-card p {
  color: #ccc;
}

.intro-card p:last-child {
  margin-bottom: 0;
}

.intro-card strong {
  color: #42b883;
  font-weight: 600;
  transition: color 0.3s ease;
}

:global(.dark) .intro-card strong {
  color: #64d8a8;
}

/* ── 时间轴 ── */
.timeline-wrapper {
  margin-bottom: 60px;
}

.subsection-title {
  font-size: clamp(18px, 2.5vw, 24px);
  margin: 0 0 32px;
  color: #333;
  font-weight: 600;
  transition: color 0.3s ease;
}

:global(.dark) .subsection-title {
  color: #e0e0e0;
}

.timeline {
  position: relative;
  padding-left: 0;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 8px;
  top: 8px;
  bottom: 8px;
  width: 2px;
  background: linear-gradient(180deg, #42b883 0%, #64d8a8 100%);
}

.timeline-item {
  position: relative;
  display: flex;
  gap: 24px;
  margin-bottom: 36px;
}

.timeline-item:last-child {
  margin-bottom: 0;
}

.timeline-marker {
  position: relative;
  flex-shrink: 0;
  width: 18px;
  display: flex;
  align-items: flex-start;
  padding-top: 2px;
}

.dot {
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background: white;
  border: 3px solid #42b883;
  box-shadow: 0 0 0 4px rgba(66,184,131,0.15);
  transition: transform 0.25s ease, box-shadow 0.25s ease, background 0.3s ease;
}

:global(.dark) .dot {
  background: #1a1a2e;
  border-color: #64d8a8;
}

.timeline-item:hover .dot {
  transform: scale(1.3);
  box-shadow: 0 0 0 6px rgba(66,184,131,0.25);
}

.timeline-content {
  flex: 1;
  background: #f9fafb;
  border-radius: 12px;
  padding: 20px 24px;
  border-left: 3px solid #42b883;
  transition: transform 0.25s ease, box-shadow 0.25s ease, background 0.3s ease, border-color 0.3s ease;
}

:global(.dark) .timeline-content {
  background: #252541;
  border-color: #64d8a8;
}

.timeline-item:hover .timeline-content {
  transform: translateX(6px);
  box-shadow: 0 6px 20px rgba(0,0,0,0.08);
}

:global(.dark) .timeline-item:hover .timeline-content {
  box-shadow: 0 6px 20px rgba(0,0,0,0.4);
}

.year {
  display: inline-block;
  background: #42b883;
  color: white;
  font-size: 13px;
  font-weight: 600;
  padding: 3px 12px;
  border-radius: 999px;
  margin-bottom: 8px;
  transition: background 0.3s ease;
}

:global(.dark) .year {
  background: #64d8a8;
  color: #1a1a2e;
}

.timeline-content h4 {
  font-size: 16px;
  color: #222;
  margin: 8px 0 6px;
  font-weight: 600;
  transition: color 0.3s ease;
}

:global(.dark) .timeline-content h4 {
  color: #e0e0e0;
}

.timeline-content p {
  font-size: 14px;
  line-height: 1.7;
  color: #555;
  margin: 0;
  transition: color 0.3s ease;
}

:global(.dark) .timeline-content p {
  color: #aaa;
}

/* ── 统计卡片 ── */
.stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 20px;
}

.stat-card {
  background: linear-gradient(135deg, #42b883 0%, #35a070 100%);
  border-radius: 14px;
  padding: 28px 24px;
  text-align: center;
  color: white;
  box-shadow: 0 6px 24px rgba(66,184,131,0.3);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  cursor: default;
}

.stat-card:hover {
  transform: translateY(-6px) scale(1.03);
  box-shadow: 0 12px 36px rgba(66,184,131,0.45);
}

.stat-value {
  font-size: clamp(32px, 4vw, 48px);
  font-weight: 700;
  margin-bottom: 8px;
  letter-spacing: 0.02em;
}

.stat-label {
  font-size: 14px;
  opacity: 0.95;
  font-weight: 500;
}

/* ── 响应式 ── */
@media (max-width: 768px) {
  .about {
    padding: 70px 6%;
  }

  .intro-card {
    padding: 24px 28px;
  }

  .timeline::before {
    left: 7px;
  }

  .timeline-item {
    gap: 16px;
  }

  .timeline-content {
    padding: 16px 20px;
  }

  .stats {
    grid-template-columns: 1fr;
  }
}
</style>
