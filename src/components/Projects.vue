<template>
  <section id="projects" class="projects">
    <h2>项目经历</h2>

    <div class="project-list">

      <div class="project-card">
        <h3>A 股日线量化回测系统</h3>

        <p>
          基于 Python + Backtrader 的量化交易平台，
          包含数据获取、双均线策略及参数优化功能。
        </p>
      </div>

      <div class="project-card">
        <h3>空气质量预测系统</h3>

        <p>
          基于 Python 的空气质量预测项目，
          包含数据清洗、建模和结果可视化。
        </p>
      </div>

    </div>
  </section>
</template>

<style scoped>
.projects {
  padding: 80px;
}

.projects h2 {
  font-size: 36px;
  margin-bottom: 30px;
}

.project-list {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.project-card {
  width: 320px;
  padding: 20px;
  border-radius: 12px;
  background: white;

  box-shadow: 0 2px 10px rgba(0,0,0,0.1);

  transition: all 0.3s;
}

.project-card:hover {
  transform: translateY(-5px);
}

.project-card p {
  line-height: 1.8;
}
</style>