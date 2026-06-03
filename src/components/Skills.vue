<script setup>
const skills = [
  { name: 'Vue3',
    level: 4},
  { name: 'JavaScript',
    level: 3},
  { name: 'Git',
    level: 4},
  { name: 'SpringBoot',
    level: 2},
]
</script>

<template>
  <section id="skills" class="skills">
    <h2>技能栈</h2>

    <div class="skill-list">
      <div class="skill-card" v-for="skill in skills" :key="skill.name">
        <div class="skill-name">{{ skill.name }}</div>
        <div class="stars">
          <span
            v-for="i in 5"
            :key="i"
            class="star"
            :class="{ filled: i <= skill.level }"
          >★</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills {
  padding: 80px;
  background: #f5f7fa;
}

.skills h2 {
  margin-bottom: 40px;
  font-size: 28px;
}

.skill-list {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.skill-card {
  padding: 24px 32px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  cursor: default;
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.skill-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 10px 24px rgba(66, 184, 131, 0.2);
}

.skill-name {
  font-size: 16px;
  font-weight: 600;
  color: #333;
}

.stars {
  display: flex;
  gap: 4px;
}

.star {
  font-size: 20px;
  color: #ddd;
  transition: transform 0.2s ease;
}

.star.filled {
  color: #42b883;
}

.skill-card:hover .star.filled {
  transform: scale(1.2);
}
</style>