<template>
  <div class="hover-copy-container" @mouseenter="showButton = true" @mouseleave="showButton = false">
    <slot></slot>
    <transition name="fade">
      <button 
        v-if="showButton" 
        class="copy-button" 
        @click="copyContent($event)"
        :title="tooltipText"
      >
        <svg 
          xmlns="http://www.w3.org/2000/svg" 
          viewBox="0 0 24 24" 
          width="16" 
          height="16"
          fill="currentColor"
        >
          <path d="M8 4V2C8 1.44772 8.44772 1 9 1H19C19.5523 1 20 1.44772 20 2V15C20 15.5523 19.5523 16 19 16H17V18.5858L21.9497 23.5355C22.1449 23.7308 22.4022 23.8415 22.6745 23.8415C22.9468 23.8415 23.2041 23.7308 23.3993 23.5355C23.5946 23.3403 23.7053 23.083 23.7053 22.8107C23.7053 22.5384 23.5946 22.2811 23.3993 22.0858L18.4645 17.151L18.4142 17.1H20C20.5523 17.1 21 16.6523 21 16.1V3C21 2.44772 20.5523 2 20 2H9C8.44772 2 8 2.44772 8 3V4H8ZM4 6V4H5V6H7V7H5V9H4V7H2V6H4ZM6 18V20H4V18H6ZM6 16H4C2.89543 16 2 16.8954 2 18V20C2 21.1046 2.89543 22 4 22H6C7.10457 22 8 21.1046 8 20V18C8 16.8954 7.10457 16 6 16ZM4 19C3.44772 19 3 18.5523 3 18C3 17.4477 3.44772 17 4 17C4.55228 17 5 17.4477 5 18C5 18.5523 4.55228 19 4 19Z"/>
        </svg>
      </button>
    </transition>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ElMessage } from 'element-plus'

const props = defineProps<{
  content?: string
  selector?: string
}>()

const showButton = ref(false)
const tooltipText = ref('复制')

const copyContent = async () => {
  try {
    let textToCopy = props.content || ''
    
    // 如果没有提供内容，但提供了选择器，则获取对应元素的文本内容
    if (!textToCopy && props.selector) {
      const element = document.querySelector(props.selector)
      if (element) {
        textToCopy = element.textContent || (element as HTMLElement).innerText || ''
      }
    }
    
    // 如果仍然没有内容，则尝试从插槽内容中获取
    if (!textToCopy) {
      const slotContent = document.querySelector('.hover-copy-container > :first-child')
      if (slotContent && slotContent !== undefined) {
        textToCopy = slotContent.textContent || (slotContent as HTMLElement).innerText || ''
      }
    }
    
    await navigator.clipboard.writeText(textToCopy)
    tooltipText.value = '已复制!'
    ElMessage.success('复制成功')
    
    // 重置提示文本
    setTimeout(() => {
      tooltipText.value = '复制'
    }, 1000)
  } catch (err) {
    console.error('复制失败:', err)
    ElMessage.error('复制失败，请手动复制')
  }
}
</script>

<style scoped>
.hover-copy-container {
  position: relative;
  display: block;
  width: 100%;
}

.copy-button {
  position: absolute;
  top: 8px;
  right: 8px;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid #dcdfe6;
  border-radius: 4px;
  cursor: pointer;
  padding: 4px;
  z-index: 10;
  transition: all 0.2s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.copy-button:hover {
  background: #f5f7fa;
  border-color: #c0c4cc;
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.copy-button:active {
  transform: translateY(0);
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>