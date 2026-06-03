<template>
  <section id="skills" class="skills">
    <h2>技能栈</h2>

    <div class="skill-list">
      <div class="skill-card">Vue3</div>
      <div class="skill-card">JavaScript</div>
      <div class="skill-card">Git</div>
      <div class="skill-card">SpringBoot</div>
    </div>
  </section>
</template>

<style scoped>
.skills {
  padding: 80px;
  background: #f5f7fa;
}

.skill-list {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.skill-card {
  padding: 20px 30px;
  background: white;
  border-radius: 10px;
}
</style>