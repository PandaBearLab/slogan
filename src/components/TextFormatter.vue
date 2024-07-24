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
      <button @click="downloadImage">下载图片</button>
      <!-- <button @click="shareToTwitter">分享到Twitter</button> -->
    </div>
    <div 
      class="output" 
      :style="outputStyle" 
      v-html="formattedText"
      ref="outputDiv"
      @mousedown="startResize"
    ></div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import html2canvas from 'html2canvas'

export default {
  name: 'TextFormatter',
  setup() {
    const input = ref('')
    const fontSize = ref(24)
    const textColor = ref('#000000')
    const bgColor = ref('#ffffff')
    const outputDiv = ref(null)
    const outputWidth = ref(400)
    const outputHeight = ref(300)

    const outputStyle = computed(() => ({
      backgroundColor: bgColor.value,
      color: textColor.value,
      fontSize: `${fontSize.value}px`,
      width: `${outputWidth.value}px`,
      height: `${outputHeight.value}px`
    }))

    const formattedText = computed(() => {
      const lines = input.value.split('\n')
      return lines
        .filter(line => line.trim() !== '')
        .map(line => {
          const randomFontSize = Math.max(fontSize.value, 24 + Math.floor(Math.random() * 24))
          return `<div class="text-block" style="font-size: ${randomFontSize}px;">${line}</div>`
        })
        .join('')
    })

    const startResize = (e) => {
      e.preventDefault()
      const startX = e.clientX
      const startY = e.clientY
      const startWidth = outputWidth.value
      const startHeight = outputHeight.value

      const resize = (e) => {
        const newWidth = startWidth + e.clientX - startX
        const newHeight = startHeight + e.clientY - startY
        outputWidth.value = Math.max(200, newWidth)
        outputHeight.value = Math.max(100, newHeight)
      }

      const stopResize = () => {
        window.removeEventListener('mousemove', resize)
        window.removeEventListener('mouseup', stopResize)
      }

      window.addEventListener('mousemove', resize)
      window.addEventListener('mouseup', stopResize)
    }

    const generateImage = async () => {
      if (outputDiv.value) {
        try {
          const canvas = await html2canvas(outputDiv.value, {
            backgroundColor: bgColor.value
          })
          return canvas.toDataURL('image/png')
        } catch (error) {
          console.error('生成图片时出错:', error)
          return null
        }
      }
      return null
    }

    const downloadImage = async () => {
      const dataUrl = await generateImage()
      if (dataUrl) {
        const link = document.createElement('a')
        link.download = '大字报.png'
        link.href = dataUrl
        link.click()
      }
    }

    const shareToTwitter = async () => {
      const dataUrl = await generateImage()
      if (dataUrl) {
        // 这里我们需要上传图片到服务器并获取URL
        // 为了演示，我们假设有一个uploadImage函数可以完成这个任务
        const imageUrl = await uploadImage(dataUrl)
        if (imageUrl) {
          const tweetText = encodeURIComponent('看看我制作的大字报！')
          const twitterUrl = `https://twitter.com/intent/tweet?text=${tweetText}&url=${encodeURIComponent(imageUrl)}`
          window.open(twitterUrl, '_blank')
        } else {
          alert('分享失败，请稍后再试。')
        }
      }
    }

    // 这个函数需要在后端实现
    const uploadImage = async (dataUrl) => {
      // 这里应该是将dataUrl上传到服务器的逻辑
      // 返回上传后的图片URL
      // 为了演示，我们返回一个假的URL
      return 'https://example.com/uploaded-image.png'
    }

    return {
      input,
      fontSize,
      textColor,
      bgColor,
      outputStyle,
      formattedText,
      outputDiv,
      startResize,
      downloadImage,
      shareToTwitter
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
  overflow: auto;
  resize: both;
  cursor: se-resize;
}

.text-block {
  margin-bottom: 10px;
}

button {
  margin-top: 10px;
  padding: 5px 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
  margin-right: 10px;
}

button:hover {
  background-color: #45a049;
}
</style>