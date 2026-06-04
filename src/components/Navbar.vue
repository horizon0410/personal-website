<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const sections = ['about', 'skills', 'projects', 'contact']
const activeSection = ref('')
const isDark = ref(false)

function updateActiveSection() {
  const scrollPos = window.scrollY + 100
  for (const id of sections) {
    const el = document.getElementById(id)
    if (el) {
      const top = el.offsetTop
      const height = el.offsetHeight
      if (scrollPos >= top && scrollPos < top + height) {
        activeSection.value = id
        return
      }
    }
  }
}

function toggleDark() {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark', isDark.value)
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
}

onMounted(() => {
  // 加载主题偏好
  const saved = localStorage.getItem('theme')
  if (saved === 'dark' || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    isDark.value = true
    document.documentElement.classList.add('dark')
  }

  updateActiveSection()
  window.addEventListener('scroll', updateActiveSection)
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateActiveSection)
})
</script>

<template>
  <nav class="navbar">
    <div class="logo">冯证杨</div>

    <ul class="nav-links">
      <li v-for="section in sections" :key="section">
        <a
          :href="`#${section}`"
          :class="{ active: activeSection === section }"
        >
          {{ section === 'about' ? '关于我' :
             section === 'skills' ? '技能' :
             section === 'projects' ? '项目' : '联系我' }}
        </a>
      </li>
    </ul>

    <button class="theme-toggle" @click="toggleDark" :aria-label="isDark ? '切换到浅色模式' : '切换到深色模式'">
      <svg v-if="!isDark" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <circle cx="12" cy="12" r="5"/>
        <line x1="12" y1="1" x2="12" y2="3"/>
        <line x1="12" y1="21" x2="12" y2="23"/>
        <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/>
        <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/>
        <line x1="1" y1="12" x2="3" y2="12"/>
        <line x1="21" y1="12" x2="23" y2="12"/>
        <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/>
        <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/>
      </svg>
      <svg v-else width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
        <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>
      </svg>
    </button>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 60px;
  background: rgba(255, 255, 255, 0.75);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 5%;
  max-width: 1400px;
  margin: 0 auto;
  box-shadow: 0 2px 16px rgba(0, 0, 0, 0.06);
  z-index: 1000;
  transition: background 0.3s ease, box-shadow 0.3s ease;
}

:global(.dark) .navbar {
  background: rgba(26, 26, 46, 0.85);
  box-shadow: 0 2px 16px rgba(0, 0, 0, 0.3);
}

.logo {
  font-size: clamp(18px, 4vw, 22px);
  font-weight: bold;
  white-space: nowrap;
  flex-shrink: 0;
  color: #1a1a2e;
  transition: color 0.3s ease;
}

:global(.dark) .logo {
  color: #fff;
}

.nav-links {
  display: flex;
  gap: clamp(8px, 2vw, 16px);
  list-style: none;
  margin: 0;
  padding: 0;
  flex-wrap: wrap;
  align-items: center;
}

.nav-links a {
  position: relative;
  text-decoration: none;
  color: #555;
  font-size: clamp(14px, 2.5vw, 15px);
  white-space: nowrap;
  padding: 6px 14px;
  border-radius: 8px;
  transition: color 0.25s ease, background 0.25s ease;
}

:global(.dark) .nav-links a {
  color: #ccc;
}

.nav-links a:hover {
  color: #42b883;
  background: rgba(66, 184, 131, 0.08);
}

:global(.dark) .nav-links a:hover {
  color: #64d8a8;
  background: rgba(100, 216, 168, 0.12);
}

.nav-links a.active {
  color: #42b883;
  background: rgba(66, 184, 131, 0.12);
  font-weight: 600;
}

:global(.dark) .nav-links a.active {
  color: #64d8a8;
  background: rgba(100, 216, 168, 0.18);
}

/* ── Theme Toggle ── */
.theme-toggle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 38px;
  height: 38px;
  border-radius: 50%;
  border: none;
  background: rgba(0, 0, 0, 0.05);
  color: #555;
  cursor: pointer;
  transition: background 0.25s ease, color 0.25s ease, transform 0.2s ease;
  margin-left: 12px;
  flex-shrink: 0;
}

.theme-toggle:hover {
  background: rgba(66, 184, 131, 0.15);
  color: #42b883;
  transform: rotate(15deg) scale(1.08);
}

:global(.dark) .theme-toggle {
  background: rgba(255, 255, 255, 0.1);
  color: #ddd;
}

:global(.dark) .theme-toggle:hover {
  background: rgba(100, 216, 168, 0.2);
  color: #64d8a8;
}

@media (max-width: 768px) {
  .navbar {
    padding: 0 3%;
  }

  .nav-links {
    gap: 6px;
  }

  .nav-links a {
    padding: 5px 10px;
    font-size: 13px;
  }

  .theme-toggle {
    width: 34px;
    height: 34px;
    margin-left: 8px;
  }
}
</style>
