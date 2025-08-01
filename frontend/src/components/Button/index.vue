<script setup lang="ts">
import type { IconType } from '@/components/Icon/index.vue'

interface Props {
  type?: 'primary' | 'normal' | 'link' | 'text'
  size?: 'default' | 'small' | 'large'
  iconSize?: number
  iconColor?: string
  icon?: IconType
  loading?: boolean
  disabled?: boolean
}

withDefaults(defineProps<Props>(), {
  type: 'normal',
  size: 'default',
  loading: false,
  disabled: false,
})
</script>

<template>
  <div
    :class="[type, size, { 'pointer-events-none': disabled || loading }]"
    class="gui-button inline-flex items-center justify-center text-center align-middle rounded-6 text-14 cursor-pointer px-12 py-6 duration-200"
  >
    <Icon v-if="loading" :fill="`var(--btn-${type}-color)`" icon="loading" class="rotation" />
    <template v-else>
      <Icon
        v-if="disabled"
        :fill="`var(--btn-${type}-color)`"
        icon="forbidden"
        class="pointer-events-none shrink-0"
      />
      <Icon
        v-if="icon"
        :icon="icon"
        :size="iconSize"
        :fill="iconColor || `var(--btn-${type}-color)`"
        :class="$slots.default ? 'mr-4' : ''"
      />
    </template>
    <slot></slot>
  </div>
</template>

<style lang="less" scoped>
.normal {
  color: var(--btn-normal-color);
  background-color: var(--btn-normal-bg);
  &:hover {
    color: var(--btn-normal-hover-color);
    border-color: var(--btn-normal-hover-border-color);
  }
  &:active {
    color: var(--btn-normal-active-color);
    border-color: var(--btn-normal-active-border-color);
  }
}

.primary {
  color: var(--btn-primary-color);
  background-color: var(--btn-primary-bg);
  border: none;
  &:hover {
    background-color: var(--btn-primary-hover-bg);
  }
  &:active {
    background-color: var(--btn-primary-active-bg);
  }
}

.link {
  color: var(--btn-link-color);
  background-color: var(--btn-link-bg);
  border: none;
  &:hover {
    color: var(--btn-link-hover-color);
  }
  &:active {
    color: var(--btn-link-active-color);
  }
}

.text {
  color: var(--btn-text-color);
  background-color: var(--btn-text-bg);
  border: none;
  &:hover {
    color: var(--btn-text-hover-color);
    background-color: var(--btn-text-hover-bg);
  }
  &:active {
    color: var(--btn-text-active-color);
    background-color: var(--btn-text-active-bg);
  }
}

.small {
  padding: 4px 8px;
  font-size: 12px;
}
.large {
  padding: 8px 12px;
  font-size: 16px;
}

.rotation {
  animation: rotate 2s infinite linear;
}
</style>
