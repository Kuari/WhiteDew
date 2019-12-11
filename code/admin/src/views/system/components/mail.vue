<template>
  <div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-tooltip class="item" effect="dark" content="配置邮箱服务后当博客有新的评论等新消息会使用邮件自动通知" placement="top-start">
          <span>邮箱设置</span>
        </el-tooltip>
        <el-switch
          v-model="openMail"
          style="float: right; padding: 3px 0"
        />
      </div>
      <div class="text">
        <el-form ref="form" :model="form" label-width="100px" :rules="rules">
          <el-form-item label="邮箱地址" prop="mail" required>
            <el-input v-model="form.mail" :disabled="!openMail" />
          </el-form-item>
          <el-form-item label="IMAP/SMTP" required>
            <el-input v-model="form.imapSmtp" prop="imapSmtp" :disabled="!openMail" />
          </el-form-item>
          <el-form-item>
            <el-button type="primary" :disabled="!openMail" @click="onSubmit">保存</el-button>
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
      openMail: false,
      form: {
        mail: '',
        imapSmtp: ''
      },
      rules: {
        mail: [
          { required: true, message: '请输入邮箱地址', trigger: 'blur' },
          { type: 'email', message: '请输入正确的邮箱地址', trigger: ['blur', 'change'] }
        ],
        imapSmtp: [
          { required: true, message: '请输入Imap/Smtp', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      console.log('submit')
    }
  }
}
</script>

<style scoped>

</style>
