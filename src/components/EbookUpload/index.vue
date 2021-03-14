<template>
  <div class="upload-container">
    <el-upload
      :action="action"
      :headers="headers"
      :multiple="false"
      :limit="1"
      :before-upload="beforeUpload"
      :on-success="onSuccess"
      :on-error="onError"
      :on-remove="onRemove"
      :on-exceed="onExceed"
      :file-list="fileList"
      :disabled="disabled"
      :show-file-list="true"
      drag
      accept="application/epub+zip"
      class="image-upload"
    >
      <i class="el-icon-upload" />
      <div v-if="fileList.length === 0" class="el-upload__text">
        将文件拖到此处，或<em>点击上传</em>
      </div>
      <div v-else class="el-upload__text">
        图书已上传
      </div>
      <!-- <div slot="tip" class="el-upload__tip">
        只能上传jpg/png文件，且不超过500kb
      </div> -->
    </el-upload>
  </div>
</template>

<script>
import { getToken } from '@/utils/auth'
export default {
  name: 'EbookUpload',
  props: {
    fileList: {
      type: Array,
      default: () => []
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      action: `${process.env.VUE_APP_BASE_API}/book/upload`
    }
  },
  computed: {
    headers() {
      return {
        Authorization: `Bearer ${getToken()}`
      }
    }
  },
  methods: {
    beforeUpload(file) {
      console.log(file)
      this.$emit('beforeUpload', file)
    },
    onSuccess() {},
    onError(err) {
      console.log({ err })
      const errMsg = err.message && JSON.parse(err.message)
      this.$message({
        message:
          (errMsg && errMsg.msg && `上传失败，失败原因：${errMsg.msg}`) ||
          '上传失败！',
        type: 'error'
      })
      this.$emit('onError', err)
    },
    onRemove() {},
    onExceed() {
      this.$message({
        message: '每次只能上传一本电子书',
        type: 'warning'
      })
    }
  }
}
</script>

<style lang="scss" scoped></style>
