// src/components/TextFormatter.vue
<template>
  <div class="text-formatter">
    <div class="controls">
      <textarea v-model="input" placeholder="在这里输入你的文本..."></textarea>
      <label>
        字体大小:
        <input type="number" v-model.number="fontSize" min="12" max="72">
      </label>
      <label>
        文本颜色:
        <input type="color" v-model="textColor">
      </label>
      <label>
        背景颜色:
        <input type="color" v-model="bgColor">
      </label>
      <button @click="generateText">生成文本</button>
    </div>
    <div class="output" :style="outputStyle" v-html="output"></div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'

export default {
  name: 'TextFormatter',
  setup() {
    const input = ref('')
    const fontSize = ref(24)
    const textColor = ref('#000000')
    const bgColor = ref('#ffffff')
    const output = ref('')

    const outputStyle = computed(() => ({
      backgroundColor: bgColor.value,
      color: textColor.value,
      fontSize: `${fontSize.value}px`
    }))

    const generateText = () => {
      const lines = input.value.split('\n')
      output.value = lines
        .filter(line => line.trim() !== '')
        .map(line => {
          const randomFontSize = 24 + Math.floor(Math.random() * 24)
          return `<div class="text-block" style="font-size: ${randomFontSize}px;">${line}</div>`
        })
        .join('')
    }

    return {
      input,
      fontSize,
      textColor,
      bgColor,
      output,
      outputStyle,
      generateText
    }
  }
}
</script>

<style scoped>
.text-formatter {
  width: 80%;
  margin: 0 auto;
}

.controls {
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 150px;
  margin-bottom: 10px;
  font-family: 'Huiwen Mingchao', Arial, sans-serif;
}

.output {
  min-height: 300px;
  border: 1px solid #ccc;
  padding: 20px;
  background-color: white;
  white-space: pre-wrap;
  word-break: break-all;
  font-family: 'Huiwen Mingchao', Arial, sans-serif;
  text-align: left;
}

.text-block {
  margin-bottom: 10px;
}
</style>
