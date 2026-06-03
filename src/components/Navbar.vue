<template>
  <nav class="navbar">
    <div class="logo">
      冯证杨
    </div>

    <ul class="nav-links">
      <li><a href="#about">关于我</a></li>
      <li><a href="#skills">技能</a></li>
      <li><a href="#projects">项目</a></li>
      <li><a href="#contact">联系我</a></li>
    </ul>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;

  height: 60px;

  background: white;

  display: flex;
  justify-content: space-between;
  align-items: center;

  padding: 0 5%;
  max-width: 1400px;
  margin: 0 auto;

  box-shadow: 0 2px 10px rgba(0,0,0,0.1);

  z-index: 1000;
}

.logo {
  font-size: clamp(18px, 4vw, 22px);
  font-weight: bold;
  white-space: nowrap;
  flex-shrink: 0;
}

.nav-links {
  display: flex;
  gap: clamp(15px, 3vw, 30px);
  list-style: none;
  margin: 0;
  padding: 0;
  flex-wrap: wrap;
  justify-content: flex-end;
}

.nav-links a {
  text-decoration: none;
  color: #333;
  font-size: clamp(14px, 2.5vw, 16px);
  white-space: nowrap;
}

@media (max-width: 768px) {
  .navbar {
    padding: 0 3%;
  }

  .nav-links {
    gap: 10px;
  }
}
</style>