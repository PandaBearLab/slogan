<template>
  <div class="container mx-auto p-4 flex flex-col lg:flex-row gap-4 max-w-screen-2xl">
    <!-- 左侧控制面板 -->
    <div class="w-full lg:w-1/3 space-y-4">
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
              <input class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
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
              <select  v-model="selectedFont" class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"  id="font-family" >
                <option v-for="(font, index) in fontFamilies" :key="index" :value="font.value" >
                  {{ font.name  }}
                  
                </option>
              </select>
            </div>
            <div class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="text-align">
                对齐方式
              </label>
              <select class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
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
              <input class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                     id="line-height" type="number" v-model.number="lineHeight" min="1" max="3" step="0.1">
            </div>
            
            <!-- 文字方向控制 -->
            <div class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="text-direction">
                文字方向
              </label>
              <select class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                      id="text-direction" v-model="textDirection">
                <option value="horizontal">横向</option>
                <option value="vertical">纵向</option>
              </select>
            </div>
            
            <!-- 背景控制 -->
            <div class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="bg-type">
                背景类型
              </label>
              <select class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
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
                <select class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
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
                <select class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
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
              <input class="w-full h-10 text-xs px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                     id="bg-image" type="file" @change="handleBgImageUpload" accept="image/*">
            </div>
          </div>
          <!-- 输出尺寸控制 -->
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="output-width">
                输出宽度 (px)
              </label>
              <input class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                    id="output-width" type="number" v-model.number="outputWidth" min="100">
            </div>
            <div class="space-y-2">
              <label class="block text-sm font-medium text-gray-700" for="output-height">
                输出高度 (px)
              </label>
              <input class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500" 
                    id="output-height" type="number" v-model.number="outputHeight" min="100">
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
        </div>
      </div>
    </div>

    <!-- 右侧预览区域 -->
    <div class="w-full lg:w-2/3">
      <div class="sticky top-4 ">
        <div class="bg-white shadow-lg rounded-lg overflow-hidden">
          <div class="p-6">
            <h3 class="text-xl font-bold text-gray-800 mb-4">预览</h3>
            <!-- 输出区域 -->
            <div class="relative" >
              <div 
                class="output border rounded-lg p-4" 
                :style="outputStyle" 
                ref="outputDiv"
                @mousedown="startResize"
              >
                <span v-if="textDirection === 'vertical'" class="vertical-text">{{ content }}</span>
                <span v-else>{{ content }}</span>
              </div>
              <div class="p-4">
                <div class="resize-handle resize-e" @mousedown="(e) => startResize(e, 'e')"></div>
                <div class="resize-handle resize-s" @mousedown="(e) => startResize(e, 's')"></div>
                <div class="resize-handle resize-se" @mousedown="(e) => startResize(e, 'se')"></div>
            </div>
              <div class="absolute bottom-0 right-0 p-1 bg-gray-200 text-xs">
                {{ outputWidth }} x {{ outputHeight }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref,reactive, computed, onMounted, onUnmounted, watch } from 'vue'
import html2canvas from 'html2canvas'



export default {
  name: 'TextFormatter',

  setup() {
    const fontSize = ref(24)
    const textColor = ref('#1D7738')
    const bgColor = ref('#ffffff')
    
    const textAlign = ref('center')
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
    const outputWidth = ref(800)
    const outputHeight = ref(600)
    const isResizing = ref(false)
    const startX = ref(0)
    const startY = ref(0)  
    const resizeDirection = ref('')
    const textDirection = ref('horizontal')
    const fontFamilies = reactive([
  { name: '汇文明朝体', value: "'汇文明朝体', serif" },
  { name: 'OPPO Sans 粗体', value: "'OPPO Sans', sans-serif" },
  { name: 'OPPO Sans 超粗体', value: "'OPPO Sans', sans-serif" },
  { name: '全字庫正楷體', value: "'全字庫正楷體', sans-serif" },
  { name: '全字庫正楷體plus', value: "'全字庫正楷體plus', sans-serif" },
  { name: '全字库简文楷体', value: "'全字库简文楷体', serif" },
  { name: '包图小白体', value: "'包图小白体', sans-serif" },
  { name: '思源黑体 极细', value: "'思源黑体', sans-serif" },
  { name: '思源黑体 超粗', value: "'思源黑体', sans-serif" },
  { name: '春风楷', value: "'春风楷', sans-serif" },
  { name: '站酷小薇LOGO体', value: "'站酷小薇LOGO体', sans-serif" },
  { name: '胡晓波男神体', value: "'胡晓波男神体', sans-serif" },
  { name: '胡晓波真帅体', value: "'胡晓波真帅体', sans-serif" },
  { name: '胡晓波骚包体', value: "'胡晓波骚包体', sans-serif" },
  { name: '贤二体', value: "'贤二体', sans-serif" }
]);

  
    const selectedFont = ref(fontFamilies[0].value)
    const fontFamily = selectedFont
   

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
        height: `${outputHeight.value}px`,
        whiteSpace: 'pre-wrap',
        wordWrap: 'break-word',
        resize: 'none',
        overflow: 'auto',
        position: 'relative',
        writingMode: textDirection.value === 'vertical' ? 'vertical-rl' : 'horizontal-tb',
        textOrientation: textDirection.value === 'vertical' ? 'upright' : 'mixed',
        fontFamilies,
        selectedFont,
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

    const startResize = (e, direction) => {
      isResizing.value = true
      resizeDirection.value = direction
      startX.value = e.clientX
      startY.value = e.clientY
      e.preventDefault()
    }

    const stopResize = () => {
      isResizing.value = false
      resizeDirection.value = ''
    }

    const resize = (e) => {
      if (!isResizing.value) return

      const deltaX = e.clientX - startX.value
      const deltaY = e.clientY - startY.value
      
      
      if (resizeDirection.value && resizeDirection.value.includes('e')) {
        outputWidth.value = Math.max(100, outputWidth.value + deltaX)
      }
      if (resizeDirection.value && resizeDirection.value.includes('s')) {
        outputHeight.value = Math.max(100, outputHeight.value + deltaY)
      }

      startX.value = e.clientX
      startY.value = e.clientY
    }

    const generateImage = async () => {
      if (!outputDiv.value) return null
      console.log(outputDiv.value)
      try {
        const canvas = await html2canvas(outputDiv.value, {
          backgroundColor: null,
          scale: 2, // 提高输出质量
          logging: false, // 禁用日志以提高性能
          useCORS: true, // 允许加载跨域图片
        })
        return canvas.toDataURL('image/png')
      } catch (error) {
        console.error('生成图片时出错:', error)
        return null
      }
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
      outputWidth.value = 800
      outputHeight.value = 600
      textDirection.value = 'horizontal'
    }

    onMounted(() => {
      if (textareaRef.value) {
        textareaRef.value.style.height = 'auto'
        textareaRef.value.style.height = `${textareaRef.value.scrollHeight}px`
      }
      window.addEventListener('mousemove', resize)
      window.addEventListener('mouseup', stopResize)
    })

    onUnmounted(() => {
      window.removeEventListener('mousemove', resize)
      window.removeEventListener('mouseup', stopResize)
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
      handleBgImageUpload,
      outputWidth,
      outputHeight,
      startResize,
      textDirection,
      selectedFont ,
      fontFamilies,
    }
  }
}
</script>

<style scoped>
.output {
  position: relative;
  overflow: hidden;
}
.resize-handle {
  position: absolute;
  background-color: #4299e1;
  opacity: 0.5;
}
.resize-e {
  top: 0;
  right: 0;
  width: 5px;
  height: 100%;
  cursor: e-resize;
}
.resize-s {
  bottom: 10;
  left: 0;
  width: 100%;
  height: 5px;
  cursor: s-resize;
}
.resize-se {
  bottom: 0;
  right: 0;
  width: 10px;
  height: 10px;
  cursor: se-resize;
}
.vertical-text {
  writing-mode: vertical-rl;
  text-orientation: upright;
}
</style>