<template>
  <div class="hero">
    <h1>你好，我是冯证杨</h1>

    <h2>Vue3 开发学习者</h2>

    <p>
      正在学习 Vue3、Git 和 Claude Code，
      目标是开发个人的博客系统。
    </p>

    <div class="buttons">
      <button>查看项目</button>
      <button>联系我</button>
    </div>
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
}

.hero {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-left: 80px;
  background: #f5f7fa;
}

.hero h1 {
  font-size: 48px;
  margin-bottom: 20px;
}

.hero h2 {
  color: #42b883;
  margin-bottom: 20px;
}

.hero p {
  width: 500px;
  line-height: 1.8;
}

.buttons {
  margin-top: 30px;
}

button {
  padding: 12px 24px;
  margin-right: 15px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}
</style>