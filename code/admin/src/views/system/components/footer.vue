<template>
  <div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>页脚信息</span>
        <el-switch
          v-model="openFooter"
          style="float: right; padding: 3px 0"
        />
      </div>
      <div class="text">
        <el-form ref="form" :model="form" label-width="80px" :rules="rules">
          <el-form-item label="页脚信息" prop="footer" required>
            <el-input
              v-model="form.footer"
              type="textarea"
              :disabled="!openFooter"
              :rows="5"
              placeholder="请输入页脚内容，支持html代码"
            />
          </el-form-item>
          <el-form-item>
            <el-button type="primary" :disabled="!openFooter" @click="onSubmit">保存</el-button>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      openFooter: false,
      form: {
        mail: '',
        imapSmtp: ''
      },
      rules: {
        footer: [
          { required: true, message: '请输入页脚信息', trigger: 'blur' }
        ]
      }
    }
  }
}
</script>

<style coped>

</style>
