<template>
  <button
    @click="toggleTheme"
    class="theme-toggle-btn"
    :class="{ 'is-light': theme === 'light' }"
    :aria-label="`Switch to ${theme === 'dark' ? 'light' : 'dark'} mode`"
  >
    <span class="theme-icon">
      <svg v-if="theme === 'dark'" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor">
        <circle cx="12" cy="12" r="5"></circle>
        <line x1="12" y1="1" x2="12" y2="3"></line>
        <line x1="12" y1="21" x2="12" y2="23"></line>
        <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
        <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
        <line x1="1" y1="12" x2="3" y2="12"></line>
        <line x1="21" y1="12" x2="23" y2="12"></line>
        <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
        <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
      </svg>
      <svg v-else width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor">
        <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
      </svg>
    </span>
    <span class="theme-label">{{ theme === 'dark' ? 'Dark' : 'Light' }}</span>
  </button>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const theme = ref('dark')

const toggleTheme = () => {
  const newTheme = theme.value === 'dark' ? 'light' : 'dark'
  theme.value = newTheme
  document.documentElement.setAttribute('data-theme', newTheme)
  localStorage.setItem('theme', newTheme)
}

onMounted(() => {
  // Check for saved theme preference or default to dark
  const savedTheme = localStorage.getItem('theme') || 'dark'
  theme.value = savedTheme
  document.documentElement.setAttribute('data-theme', savedTheme)
})
</script>

<style scoped>
.theme-toggle-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.25rem;
  background: rgba(26, 26, 26, 0.95);
  border: 1px solid rgba(0, 255, 255, 0.3);
  border-radius: 50px;
  color: var(--text-secondary);
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
  font-size: 0.875rem;
  font-weight: 500;
  letter-spacing: 0.05em;
}

.theme-toggle-btn:hover {
  border-color: var(--neon-cyan);
  color: var(--neon-cyan);
  box-shadow: 0 0 20px rgba(0, 255, 255, 0.3);
}

.theme-toggle-btn.is-light {
  background: rgba(255, 255, 255, 0.95);
  border-color: rgba(0, 128, 128, 0.3);
}

.theme-toggle-btn.is-light:hover {
  border-color: var(--neon-cyan);
  box-shadow: 0 0 20px rgba(0, 128, 128, 0.3);
}

.theme-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 24px;
  height: 24px;
}

.theme-icon svg {
  stroke-width: 2;
}

.theme-label {
  text-transform: uppercase;
  font-size: 0.75rem;
}
</style>