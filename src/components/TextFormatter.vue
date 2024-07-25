<template>
  <div class="container mx-auto p-4 max-w-4xl">
    <div class="bg-white shadow-lg rounded-lg overflow-hidden">
      <div class="p-6 space-y-6">
        <h2 class="text-2xl font-bold text-gray-800 mb-4">文本排版工具</h2>
        
        <!-- 控制区域 -->
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
          <!-- 字体控制 -->
          <div class="space-y-2">
            <label class="block text-sm font-medium text-gray-700" for="font-size">
              字体大小
            </label>
            <input class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                   id="font-size" type="number" v-model.number="fontSize" min="12" max="72">
          </div>
          <div class="space-y-2">
            <label class="block text-sm font-medium text-gray-700" for="text-color">
              文本颜色
            </label>
            <input class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                   id="text-color" type="color" v-model="textColor">
          </div>
          <div class="space-y-2">
            <label class="block text-sm font-medium text-gray-700" for="font-family">
              字体
            </label>
            <select class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                    id="font-family" v-model="fontFamily">
              <option value="'Huiwen Mingchao', Arial, sans-serif">明朝体</option>
              <option value="'SimHei', Arial, sans-serif">黑体</option>
              <option value="'KaiTi', Arial, sans-serif">楷体</option>
              <option value="'FangSong', Arial, sans-serif">仿宋</option>
            </select>
          </div>
          <div class="space-y-2">
            <label class="block text-sm font-medium text-gray-700" for="text-align">
              对齐方式
            </label>
            <select class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                    id="text-align" v-model="textAlign">
              <option value="left">左对齐</option>
              <option value="center">居中</option>
              <option value="right">右对齐</option>
              <option value="justify">两端对齐</option>
            </select>
          </div>
          <div class="space-y-2">
            <label class="block text-sm font-medium text-gray-700" for="line-height">
              行间距
            </label>
            <input class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                   id="line-height" type="number" v-model.number="lineHeight" min="1" max="3" step="0.1">
          </div>
          
          <!-- 背景控制 -->
          <div class="space-y-2">
            <label class="block text-sm font-medium text-gray-700" for="bg-type">
              背景类型
            </label>
            <select class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                    id="bg-type" v-model="bgType">
              <option value="solid">纯色</option>
              <option value="gradient">渐变色</option>
              <option value="image">图片</option>
            </select>
          </div>
          
          <div v-if="bgType === 'solid'" class="space-y-2">
            <label class="block text-sm font-medium text-gray-700" for="bg-color">
              背景颜色
            </label>
            <input class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                   id="bg-color" type="color" v-model="bgColor">
          </div>
          
          <template v-if="bgType === 'gradient'">
            <div class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="gradient-type">
                渐变类型
              </label>
              <select class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                      id="gradient-type" v-model="gradientType">
                <option value="linear">线性渐变</option>
                <option value="radial">径向渐变</option>
              </select>
            </div>
            <div class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="gradient-color-1">
                渐变颜色1
              </label>
              <input class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                     id="gradient-color-1" type="color" v-model="gradientColor1">
            </div>
            <div class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="gradient-color-2">
                渐变颜色2
              </label>
              <input class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                     id="gradient-color-2" type="color" v-model="gradientColor2">
            </div>
            <div v-if="gradientType === 'linear'" class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="gradient-direction">
                渐变方向
              </label>
              <select class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                      id="gradient-direction" v-model="gradientDirection">
                <option value="to right">从左到右</option>
                <option value="to bottom">从上到下</option>
                <option value="to bottom right">左上到右下</option>
                <option value="to bottom left">右上到左下</option>
              </select>
            </div>
          </template>
          
          <div v-if="bgType === 'image'" class="space-y-2">
            <label class="block text-sm font-medium text-gray-700" for="bg-image">
              背景图片
            </label>
            <input class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                   id="bg-image" type="file" @change="handleBgImageUpload" accept="image/*">
          </div>
        </div>
        
        <!-- 操作按钮 -->
        <div class="flex flex-wrap gap-4">
          <button @click="downloadImage" class="px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 transition-colors duration-300">
            下载图片
          </button>
          <button @click="resetSettings" class="px-4 py-2 bg-gray-600 text-white rounded-md hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-gray-500 focus:ring-offset-2 transition-colors duration-300">
            重置设置
          </button>
        </div>
        
        <!-- 输入区域 -->
        <textarea
          ref="textareaRef"
          v-model="content"
          class="w-full p-4 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 transition-shadow duration-300"
          :style="{ resize: 'vertical', minHeight: '100px' }"
          rows="5"
        ></textarea>
        
        <!-- 输出区域 -->
        <div 
          class="output border rounded-lg p-4" 
          :style="outputStyle" 
          ref="outputDiv"
        >{{ content }}</div>
      </div>
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
    const textareaRef = ref(null)
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
        width: '100%',
        minHeight: '300px',
        maxHeight: 'none',
        whiteSpace: 'pre-wrap',
        wordWrap: 'break-word'
      }
    })

    const handleBgImageUpload = (e) => {
      const file = e.target.files[0]
      if (file) {
        const reader = new FileReader()
        reader.onload = (e) => bgImage.value = e.target.result
        reader.readAsDataURL(file)
      }
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
      content.value = '在这里输入你的文本...'
      bgType.value = 'solid'
      gradientType.value = 'linear'
      gradientColor1.value = '#ffffff'
      gradientColor2.value = '#000000'
      gradientDirection.value = 'to right'
      bgImage.value = ''
    }

    onMounted(() => {
      if (textareaRef.value) {
        textareaRef.value.style.height = 'auto'
        textareaRef.value.style.height = `${textareaRef.value.scrollHeight}px`
      }
    })

    watch(content, () => {
      if (textareaRef.value) {
        textareaRef.value.style.height = 'auto'
        textareaRef.value.style.height = `${textareaRef.value.scrollHeight}px`
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
      textareaRef,
      content,
      downloadImage,
      resetSettings,
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

<style scoped>
.output {
  position: relative;
  overflow: auto;
}
</style>