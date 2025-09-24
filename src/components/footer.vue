<script>
const company = "ilhamxkz"

</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="left">
        <slot name="brand">
          <div class="brand">{{ company }}</div>
        </slot>
        <div class="small">© {{ year }} {{ company }}. All rights reserved.</div>
      </div>

      <nav class="links" v-if="links && links.length">
        <a v-for="(l, i) in links" :key="i" :href="l.href" target="_blank" rel="noopener">{{ l.label }}</a>
      </nav>

      <div class="right">
        <slot name="extra">
          <div v-if="showCredit" class="credit">Made with ♥</div>
        </slot>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  company: { type: String, default: 'Nama Perusahaan' },
  links: { type: Array, default: () => [] },
  showCredit: { type: Boolean, default: true },
  startYear: { type: [Number, String], default: null }
})

const year = computed(() => {
  const now = new Date().getFullYear()
  return props.startYear ? `${props.startYear} - ${now}` : now
})
</script>

<style scoped>
.footer {
  border-top: 1px solid #e5e7eb;
  padding: 18px 16px;
  margin: 12px;
  background: #fafafa;
  color: #374151;
  font-size: 14px;
  border-radius: 6px;
  box-shadow: 0 9px 23px rgba(0, 0, 0, 0.12);
}
.container {
  max-width: 1100px;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;

}
.left {
  display: flex;
  flex-direction: column;
}
.brand {
  font-weight: 700;
}
.small {
  font-size: 12px;
  color: #6b7280;
}
.links a {
  margin-left: 12px;
  text-decoration: none;
  color: inherit;
  font-size: 14px;
}
.credit {
  font-size: 13px;
  color: #6b7280;
}

@media (max-width: 640px) {
  .container { flex-direction: column; align-items: flex-start; }
  .links { margin-top: 8px; }
}
</style>

