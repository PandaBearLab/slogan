<template>
  <div class="container mx-auto p-4">
    <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
      <div class="mb-4 flex flex-wrap gap-4">
        <!-- Existing controls -->
        <div class="w-full md:w-auto">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="font-size">
            字体大小
          </label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                 id="font-size" type="number" v-model.number="fontSize" min="12" max="72">
        </div>
        <div class="w-full md:w-auto">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="text-color">
            文本颜色
          </label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                 id="text-color" type="color" v-model="textColor">
        </div>
        <div class="w-full md:w-auto">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="font-family">
            字体
          </label>
          <select class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                  id="font-family" v-model="fontFamily">
            <option value="'Huiwen Mingchao', Arial, sans-serif">明朝体</option>
            <option value="'SimHei', Arial, sans-serif">黑体</option>
            <option value="'KaiTi', Arial, sans-serif">楷体</option>
            <option value="'FangSong', Arial, sans-serif">仿宋</option>
          </select>
        </div>
        <div class="w-full md:w-auto">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="text-align">
            对齐方式
          </label>
          <select class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                  id="text-align" v-model="textAlign">
            <option value="left">左对齐</option>
            <option value="center">居中</option>
            <option value="right">右对齐</option>
            <option value="justify">两端对齐</option>
          </select>
        </div>
        <div class="w-full md:w-auto">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="line-height">
            行间距
          </label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                 id="line-height" type="number" v-model.number="lineHeight" min="1" max="3" step="0.1">
        </div>
        
        <!-- New background controls -->
        <div class="w-full md:w-auto">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="bg-type">
            背景类型
          </label>
          <select class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                  id="bg-type" v-model="bgType">
            <option value="solid">纯色</option>
            <option value="gradient">渐变色</option>
            <option value="image">图片</option>
          </select>
        </div>
        
        <div v-if="bgType === 'solid'" class="w-full md:w-auto">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="bg-color">
            背景颜色
          </label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                 id="bg-color" type="color" v-model="bgColor">
        </div>
        
        <template v-if="bgType === 'gradient'">
          <div class="w-full md:w-auto">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="gradient-type">
              渐变类型
            </label>
            <select class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                    id="gradient-type" v-model="gradientType">
              <option value="linear">线性渐变</option>
              <option value="radial">径向渐变</option>
            </select>
          </div>
          <div class="w-full md:w-auto">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="gradient-color-1">
              渐变颜色1
            </label>
            <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                   id="gradient-color-1" type="color" v-model="gradientColor1">
          </div>
          <div class="w-full md:w-auto">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="gradient-color-2">
              渐变颜色2
            </label>
            <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                   id="gradient-color-2" type="color" v-model="gradientColor2">
          </div>
          <div v-if="gradientType === 'linear'" class="w-full md:w-auto">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="gradient-direction">
              渐变方向
            </label>
            <select class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                    id="gradient-direction" v-model="gradientDirection">
              <option value="to right">从左到右</option>
              <option value="to bottom">从上到下</option>
              <option value="to bottom right">左上到右下</option>
              <option value="to bottom left">右上到左下</option>
            </select>
          </div>
        </template>
        
        <div v-if="bgType === 'image'" class="w-full md:w-auto">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="bg-image">
            背景图片
          </label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
                 id="bg-image" type="file" @change="handleBgImageUpload" accept="image/*">
        </div>
      </div>
      
      <div class="flex flex-wrap gap-4 mb-4">
        <button @click="downloadImage" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
          下载图片
        </button>
        <button @click="resetSettings" class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
          重置设置
        </button>
      </div>
      
      <div 
        class="output border rounded p-4 focus:outline-none focus:shadow-outline" 
        :style="outputStyle" 
        ref="outputDiv"
        contenteditable="true"
        @input="updateContent"
        @mousedown="startResize"
        v-html="formattedContent"
      ></div>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted, watch } from 'vue'
import html2canvas from 'html2canvas'

export default {
  name: 'TextFormatter',
  setup() {
    const fontSize = ref(24)
    const textColor = ref('#1D7738')
    const bgColor = ref('#ffffff')
    const fontFamily = ref("'Huiwen Mingchao', Arial, sans-serif")
    const textAlign = ref('left')
    const lineHeight = ref(1.5)
    const outputDiv = ref(null)
    const outputWidth = ref(400)
    const outputHeight = ref(300)
    const content = ref('在这里输入你的文本...')
    const bgType = ref('solid')
    const gradientType = ref('linear')
    const gradientColor1 = ref('#ffffff')
    const gradientColor2 = ref('#000000')
    const gradientDirection = ref('to right')
    const bgImage = ref('')

    const outputStyle = computed(() => {
      let backgroundValue = bgColor.value
      if (bgType.value === 'gradient') {
        backgroundValue = `${gradientType.value}-gradient(${gradientDirection.value}, ${gradientColor1.value}, ${gradientColor2.value})`
      } else if (bgType.value === 'image' && bgImage.value) {
        backgroundValue = `url(${bgImage.value}) center/cover no-repeat`
      }
      
      return {
        backgroundColor: bgType.value === 'solid' ? bgColor.value : 'transparent',
        background: backgroundValue,
        color: textColor.value,
        fontSize: `${fontSize.value}px`,
        fontFamily: fontFamily.value,
        textAlign: textAlign.value,
        lineHeight: lineHeight.value,
        width: `${outputWidth.value}px`,
        minHeight: `${outputHeight.value}px`,
        maxHeight: 'none'
      }
    })

    const formattedContent = computed(() => {
      return content.value
    })

    const startResize = (e) => {
      const rect = outputDiv.value.getBoundingClientRect()
      const isResizeArea = (e.clientX > rect.right - 20 && e.clientY > rect.bottom - 20)
      if (!isResizeArea) return

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

    const updateContent = (e) => {
      content.value = e.target.innerHTML
    }

    const generateImage = async () => {
      if (outputDiv.value) {
        try {
          const canvas = await html2canvas(outputDiv.value, {
            backgroundColor: null
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
        link.download = '文字排版.png'
        link.href = dataUrl
        link.click()
      }
    }

    const resetSettings = () => {
      fontSize.value = 24
      textColor.value = '#1D7738'
      bgColor.value = '#ffffff'
      fontFamily.value = "'Huiwen Mingchao', Arial, sans-serif"
      textAlign.value = 'left'
      lineHeight.value = 1.5
      outputWidth.value = 400
      outputHeight.value = 300
      content.value = '在这里输入你的文本...'
      bgType.value = 'solid'
      gradientType.value = 'linear'
      gradientColor1.value = '#ffffff'
      gradientColor2.value = '#000000'
      gradientDirection.value = 'to right'
      bgImage.value = ''
    }

    const handleBgImageUpload = (e) => {
      const file = e.target.files[0]
      if (file) {
        const reader = new FileReader()
        reader.onload = (e) => bgImage.value = e.target.result
        reader.readAsDataURL(file)
      }
    }

    onMounted(() => {
      if (outputDiv.value) {
        outputDiv.value.innerHTML = content.value
      }
    })

    watch([fontSize, textColor, bgColor, fontFamily, textAlign, lineHeight, bgType, gradientType, gradientColor1, gradientColor2, gradientDirection, bgImage], () => {
      if (outputDiv.value) {
        outputDiv.value.innerHTML = content.value
      }
    })

    return {
      fontSize,
      textColor,
      bgColor,
      fontFamily,
      textAlign,
      lineHeight,
      outputStyle,
      outputDiv,
      formattedContent,
      startResize,
      downloadImage,
      resetSettings,
      updateContent,
      bgType,
      gradientType,
      gradientColor1,
      gradientColor2,
      gradientDirection,
      bgImage,
      handleBgImageUpload
    }
  }
}
</script>

<style>
@import 'https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css';

.output {
  white-space: pre-wrap;
  word-break: break-word;
  overflow-wrap: break-word;
  cursor: text;
  position: relative;
}

.output::after {
  content: '';
  position: absolute;
  right: 0;
  bottom: 0;
  width: 20px;
  height: 20px;
  cursor: se-resize;
}
</style>