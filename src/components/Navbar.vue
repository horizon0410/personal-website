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

  width: 100%;

  height: 60px;

  background: white;

  display: flex;
  justify-content: space-between;
  align-items: center;

  padding: 0 40px;

  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  
  z-index: 1000;
}

.logo {
  font-size: 22px;
  font-weight: bold;
}

.nav-links {
  display: flex;
  gap: 30px;

  list-style: none;
}

.nav-links a {
  text-decoration: none;
  color: #333;
}
</style>