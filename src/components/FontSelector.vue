<template>
    <div class="font-selector"  >
      <select 
        v-model="selectedFont" 
    
        class="w-full h-10 px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"  id="font-family" 
      >
        <option 
          v-for="(font, index) in fontFamilies" 
          :key="index" 
          :value="font.value"
        >
          {{ font.name }}
        </option>
      </select>
      
      <!-- <div 
        class="mt-4 p-4 border rounded"
        :style="{ fontFamily: selectedFont, fontSize: '18px' }"
      >
        这是使用所选字体的示例文本。
        The quick brown fox jumps over the lazy dog.
      </div> -->
    </div>
  </template>
  
  <script>
  import { ref, reactive } from 'vue'
  
  export default {
    name: 'FontSelector',
    setup() {
        const fontFamilies = reactive([
            { name: '汇文明朝体', value: '汇文明朝体, serif' },
            { name: 'OPPO Sans Bold', value: 'OPPO Sans, sans-serif' },
            { name: 'OPPO Sans Heavy', value: 'OPPO Sans, sans-serif' },
            { name: '全字库正黑体', value: '全字库正黑体, sans-serif' },
            { name: '全字库正黑体Plus', value: '全字库正黑体Plus, sans-serif' },
            { name: '全字库简文楷体', value: '全字库简文楷体, serif' },
            { name: '包圆小白体', value: '包圆小白体, sans-serif' },
            { name: '思源黑体 ExtraLight', value: '思源黑体, sans-serif' },
            { name: '思源黑体 Heavy', value: '思源黑体, sans-serif' },
            { name: '麻手锋黑体', value: '麻手锋黑体, sans-serif' },
            { name: '调英风格体', value: '调英风格体, sans-serif' },
            { name: '站酷小薇LOGO体', value: '站酷小薇LOGO体, sans-serif' },
            { name: '胡晓波男神体', value: '胡晓波男神体, sans-serif' },
            { name: '胡晓波金凯体', value: '胡晓波金凯体, sans-serif' },
            { name: '胡晓波浪漫体', value: '胡晓波浪漫体, cursive' },
            { name: '贤二体', value: '贤二体, sans-serif' }
            ]);
  
      const selectedFont = ref(fontFamilies[0].value)
  
      return {
        fontFamilies,
        selectedFont
      }
    }
  }
  </script>
  
  <style scoped>
  .font-selector {
    /* 可以根据需要添加样式 */
  }
  </style>