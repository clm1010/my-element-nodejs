<template>
  <el-form ref="postForm" :model="postForm">
    <!-- <sticky :class-name="'sub-navbar ' + postForm.status"> -->
    <sticky :class-name="'sub-navbar '">
      <el-button v-if="!isEdit" @click="showGuide">显示帮助</el-button>
      <el-button
        type="success"
        :loading="loading"
        style="margin-left: 10px;"
        @click="submitForm"
      >
        {{ isEdit ? '编辑电子书' : '新增电子书' }}
      </el-button>
    </sticky>
    <!-- 表单容器 -->
    <div class="detail-container">
      <el-row>
        <warning />
        <el-col :span="24">
          <ebook-upload />
        </el-col>
        <!-- 表单控件的具体样式 -->
        <el-col :span="24">123</el-col>
      </el-row>
    </div>
  </el-form>
</template>

<script>
import Sticky from '@/components/Sticky/index'
import EbookUpload from '@/components/EbookUpload'
import Warning from './Warning'

export default {
  name: 'Detail',
  components: {
    Sticky,
    Warning,
    EbookUpload
  },
  props: {
    isEdit: Boolean
  },
  data() {
    return {
      loading: false,
      postForm: {
        // status: 'draft' //draft deleted 状态
      }
    }
  },
  methods: {
    showGuide() {
      console.log('show guide')
    },
    submitForm() {
      console.log('submitForm')
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 1000)
    }
  }
}
</script>

<style lang="scss" scoped>
.detail-container {
  padding: 40px 50px 20px;
}
</style>
