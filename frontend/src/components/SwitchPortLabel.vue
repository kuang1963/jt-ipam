<script setup lang="ts">
/**
 * 交換器位置顯示：把「switch-003 / eth1/0/24」呈現為「switch-003@eth1/0/24」，
 * 其中 @ 用品牌色標示。只切第一個 " / "（port 內含的斜線如 eth1/0/24 不動）。
 */
import { computed } from "vue";

const props = defineProps<{ value?: string | null; dim?: boolean }>();

const parts = computed<{ sw: string; port: string | null }>(() => {
  const v = (props.value ?? "").trim();
  const idx = v.indexOf(" / ");
  if (idx < 0) return { sw: v, port: null };
  return { sw: v.slice(0, idx), port: v.slice(idx + 3) };
});
</script>

<template>
  <span v-if="parts.sw" class="swp" :class="{ dim }">
    {{ parts.sw }}<template v-if="parts.port"><span class="swp-at">@</span>{{ parts.port }}</template>
  </span>
</template>

<style scoped>
.swp.dim { color: var(--n-text-color-3, #888); }
.swp-at { color: #18a058; font-weight: 700; margin: 0 1px; }
</style>
