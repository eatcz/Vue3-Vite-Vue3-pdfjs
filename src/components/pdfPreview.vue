<template>
  <div class="pdfPreview h-screen p-5" id="pdfPreview">
    <vue-pdf-embed
      :source="state.source"
      :style="state.scale"
      class="vue-pdf-embed"
    />
  </div>
</template>

<script setup lang="ts">
import { reactive, onMounted, computed } from "vue";
import VuePdfEmbed from "vue-pdf-embed";
import { createLoadingTask } from "vue3-pdfjs/esm";
const props = defineProps({
  pdfUrl: {
    type: String,
    required: true,
  },
});

const state = reactive({
  source:
    "https://mozilla.github.io/pdf.js/web/compressed.tracemonkey-pldi-09.pdf",
  //预览pdf文件地址
  pageNum: 1, //当前页
  scale: 1, //缩放比例
  numPages: 0, //总页数
});

// 获取预览文件
onMounted(() => {
  const loadingTask = createLoadingTask(state.source);
  loadingTask.promise.then((pdf: { numPages: number }) => {
    state.numPages = pdf.numPages;
  });
});
</script>

<style scoped>
</style>