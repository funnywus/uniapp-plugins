<template>
  <view class="content">
    <button @click="pickFile">选择文件</button>
    <view v-if="fileInfo" class="file-info">
      <text>文件名：{{fileInfo.fileName}}</text>
      <text class="path-text">路径：{{fileInfo.path}}</text>
      <text>后缀：{{fileInfo.extension}}</text>
      <image v-if="isImage" :src="fileInfo.path" class="preview-image"></image>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      fileInfo: null
    }
  },
  computed: {
    isImage() {
      return this.fileInfo && ['jpg', 'jpeg', 'png', 'gif'].includes(this.fileInfo.extension.toLowerCase());
    }
  },
  methods: {
    pickFile() {
      const filePicker = uni.requireNativePlugin('FilePicker')
      filePicker.pickFile({}, result => {
        if (result.success) {
          this.fileInfo = {
            fileName: result.fileName,
            path: result.path,
            extension: result.extension
          }
        } else {
          uni.showToast({
            title: result.message || '选择文件失败',
            icon: 'none'
          })
        }
      })
    }
  }
}
</script>

<style>
.content {
  padding: 20px;
}
.file-info {
  margin-top: 20px;
}
.file-info text {
  display: block;
  margin: 5px 0;
}
.preview-image {
  width: 100px;
  height: 100px;
  margin-top: 10px;
}
.path-text {
  word-break: break-all;
  white-space: normal;
}
</style>