<template>
  <section id="contact" class="contact">
    <h2>联系我</h2>

    <p>欢迎交流学习与项目开发经验。</p>

    <div class="contact-info">
      <p>📧 邮箱：Qw1131740167@163.com</p>
      <p>💻 GitHub：github.com/horizon0410</p>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: 80px;
  background: #f5f7fa;
  transition: background 0.3s ease;
}

:global(.dark) .contact {
  background: #1a1a2e;
}

.contact h2 {
  font-size: 36px;
  margin-bottom: 20px;
  color: #1a1a2e;
  transition: color 0.3s ease;
}

:global(.dark) .contact h2 {
  color: #fff;
}

.contact > p {
  color: #555;
  transition: color 0.3s ease;
}

:global(.dark) .contact > p {
  color: #bbb;
}

.contact-info {
  margin-top: 20px;
}

.contact-info p {
  margin-bottom: 12px;
  font-size: 18px;
  color: #333;
  transition: color 0.3s ease;
}

:global(.dark) .contact-info p {
  color: #ccc;
}
</style>