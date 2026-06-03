<template>
  <section class="hero">  

    <div class="hero-content">

      <div class="hero-text">
        <h1>你好，我是冯证杨</h1>

        <h2>Vue3 开发学习者</h2>

        <p>
          正在学习 Vue3、Git、前端工程化与项目部署，
          目前努力开发个人博客系统。
        </p>

        <div class="buttons">
          <button>查看项目</button>
          <button>联系我</button>
        </div>
      </div>

      <div class="hero-avatar">
        FZY
      </div>

    </div>

  </section>
</template>

<style scoped>
.hero {
  height: 100vh;
  display: flex;
  align-items: center;
  padding: 0 10%;

  background: linear-gradient(
  135deg,
  #f5f7fa 0%,
  #e8f4ff 100%
);

  padding-top: 60px; /* 给固定导航栏留空间 */
}

.hero-content {
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
  gap: 15px;
}

.buttons button {
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 15px;
  transition: all .3s;
}

.buttons button:first-child {
  background: #42b883;
  color: white;
}

.buttons button:last-child {
  background: white;
  color: #333;
  border: 1px solid #ddd;
}

.hero-avatar {
  width: clamp(100px, 18vw, 200px);
  height: clamp(100px, 18vw, 200px);
  border-radius: 50%;
  background: #42b883;
  box-shadow: 0 10px 30px rgba(66,184,131,.3);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: clamp(24px, 5vw, 48px);
  font-weight: bold;
  flex-shrink: 0;
  animation: float 3s ease-in-out infinite;
}
.buttons button:hover {
    transform: translateY(-3px);
  }

@media (max-width: 768px) {
  .hero {
    padding: 80px 6% 40px;
  }

  .hero-content {
    flex-direction: column-reverse;
    text-align: center;
  }

  .buttons {
    justify-content: center;
  }
}
@keyframes float {
  0% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-10px);
  }

  100% {
    transform: translateY(0);
  }
}
</style>