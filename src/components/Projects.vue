<script setup>
import { ref } from 'vue'

const projects = [
  {
    name: 'A 股日线量化回测系统',
    summary: '基于 Python + Backtrader 的量化交易平台，包含数据获取、双均线策略及参数优化功能。',
    tags: ['Python', 'Backtrader', 'Pandas', 'Matplotlib'],
    features: [
      '自动从 Tushare 获取 A 股日线数据',
      '实现双均线（MA5/MA20）交叉策略',
      '支持参数网格搜索与最优组合输出',
      '收益曲线与回撤可视化图表',
    ],
    github: '',
  },
  {
    name: '空气质量预测系统',
    summary: '基于 Python 的空气质量预测项目，包含数据清洗、建模和结果可视化。',
    tags: ['Python', 'Scikit-learn', 'Pandas', 'Seaborn'],
    features: [
      '多源气象与污染数据清洗与合并',
      '随机森林模型训练与交叉验证',
      'AQI 指数多步预测',
      '特征重要性热力图可视化',
    ],
    github: '',
  },
]

const active = ref(null)
const open = (project) => { active.value = project }
const close = () => { active.value = null }
</script>

<template>
  <section id="projects" class="projects">
    <h2>项目经历</h2>

    <div class="project-list">
      <div
        class="project-card"
        v-for="project in projects"
        :key="project.name"
      >
        <h3>{{ project.name }}</h3>

        <p>{{ project.summary }}</p>

        <div class="tags">
          <span class="tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
        </div>

        <button class="detail-btn" @click="open(project)">查看详情</button>
      </div>
    </div>

    <!-- 详情弹窗 -->
    <Transition name="fade">
      <div class="modal-mask" v-if="active" @click.self="close">
        <div class="modal">
          <button class="close-btn" @click="close">✕</button>

          <h3>{{ active.name }}</h3>

          <p class="modal-summary">{{ active.summary }}</p>

          <div class="tags">
            <span class="tag" v-for="tag in active.tags" :key="tag">{{ tag }}</span>
          </div>

          <h4>主要功能</h4>
          <ul>
            <li v-for="feat in active.features" :key="feat">{{ feat }}</li>
          </ul>

          <a
            v-if="active.github"
            :href="active.github"
            target="_blank"
            class="github-link"
          >查看源码 →</a>
        </div>
      </div>
    </Transition>
  </section>
</template>

<style scoped>
.projects {
  padding: 80px;
  background: #f9fafb;
  transition: background 0.3s ease;
}

:global(.dark) .projects {
  background: #16213e;
}

.projects h2 {
  font-size: 36px;
  margin-bottom: 40px;
  color: #1a1a2e;
  transition: color 0.3s ease;
}

:global(.dark) .projects h2 {
  color: #fff;
}

.project-list {
  display: flex;
  gap: 24px;
  flex-wrap: wrap;
}

.project-card {
  width: 320px;
  padding: 28px;
  border-radius: 14px;
  background: white;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
  display: flex;
  flex-direction: column;
  gap: 14px;
  transition: transform 0.25s ease, box-shadow 0.25s ease, background 0.3s ease;
}

:global(.dark) .project-card {
  background: #252541;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.4);
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 28px rgba(66, 184, 131, 0.18);
}

:global(.dark) .project-card:hover {
  box-shadow: 0 12px 28px rgba(100, 216, 168, 0.25);
}

.project-card h3 {
  margin: 0;
  font-size: 18px;
  color: #222;
  transition: color 0.3s ease;
}

:global(.dark) .project-card h3 {
  color: #e0e0e0;
}

.project-card p {
  margin: 0;
  line-height: 1.8;
  color: #555;
  font-size: 14px;
  flex: 1;
  transition: color 0.3s ease;
}

:global(.dark) .project-card p {
  color: #aaa;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tag {
  background: #e8f7f0;
  color: #42b883;
  font-size: 12px;
  padding: 3px 10px;
  border-radius: 20px;
  font-weight: 500;
  transition: background 0.3s ease, color 0.3s ease;
}

:global(.dark) .tag {
  background: rgba(100,216,168,0.15);
  color: #64d8a8;
}

.detail-btn {
  align-self: flex-start;
  padding: 8px 20px;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  transition: background 0.2s ease, transform 0.2s ease;
}

.detail-btn:hover {
  background: #33a06f;
  transform: translateY(-2px);
}

:global(.dark) .detail-btn {
  background: #64d8a8;
  color: #1a1a2e;
}

:global(.dark) .detail-btn:hover {
  background: #52c896;
}

/* 弹窗 */
.modal-mask {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.45);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  transition: background 0.3s ease;
}

:global(.dark) .modal-mask {
  background: rgba(0, 0, 0, 0.7);
}

.modal {
  background: white;
  border-radius: 16px;
  padding: 40px;
  width: 90%;
  max-width: 520px;
  position: relative;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.2);
  transition: background 0.3s ease, box-shadow 0.3s ease;
}

:global(.dark) .modal {
  background: #252541;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.6);
}

.modal h3 {
  font-size: 22px;
  margin: 0 0 12px;
  color: #222;
  transition: color 0.3s ease;
}

:global(.dark) .modal h3 {
  color: #e0e0e0;
}

.modal-summary {
  color: #555;
  line-height: 1.8;
  margin: 0 0 16px;
  font-size: 15px;
  transition: color 0.3s ease;
}

:global(.dark) .modal-summary {
  color: #aaa;
}

.modal h4 {
  margin: 20px 0 10px;
  font-size: 15px;
  color: #333;
  transition: color 0.3s ease;
}

:global(.dark) .modal h4 {
  color: #ccc;
}

.modal ul {
  padding-left: 20px;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.modal ul li {
  color: #555;
  line-height: 1.7;
  font-size: 14px;
  transition: color 0.3s ease;
}

:global(.dark) .modal ul li {
  color: #aaa;
}

.github-link {
  display: inline-block;
  margin-top: 24px;
  color: #42b883;
  font-weight: 600;
  text-decoration: none;
  font-size: 14px;
  transition: color 0.3s ease;
}

:global(.dark) .github-link {
  color: #64d8a8;
}

.github-link:hover {
  text-decoration: underline;
}

.close-btn {
  position: absolute;
  top: 16px;
  right: 20px;
  background: none;
  border: none;
  font-size: 18px;
  cursor: pointer;
  color: #999;
  line-height: 1;
  transition: color 0.2s;
}

.close-btn:hover {
  color: #333;
}

:global(.dark) .close-btn {
  color: #888;
}

:global(.dark) .close-btn:hover {
  color: #ddd;
}

/* 过渡动画 */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>