<template>
  <div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>系统设置</span>
      </div>
      <div class="text">
        <el-form ref="form" :model="systemSettingForm" label-width="80px" :rules="systemRules">
          <el-form-item label="网站名称" prop="name" required>
            <el-input v-model="systemSettingForm.name" />
          </el-form-item>
          <el-form-item label="网站地址" required>
            <el-input v-model="systemSettingForm.domain" placeholder="请输入内容" prop="domain">
              <el-select slot="prepend" v-model="systemSettingForm.protocol" placeholder="请选择" class="protocolSelect">
                <el-option label="https://" value="1" />
                <el-option label="http://" value="2" />
              </el-select>
            </el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="onSystemSettingSubmit">保存</el-button>
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
      systemSettingForm: {
        name: '白露',
        protocol: '1',
        domain: 'www.justmylife.cc'
      },
      systemRules: {
        name: [
          { required: true, message: '请输入博客名', trigger: 'blur' }
        ],
        domain: [
          { required: true, message: '请输入域名', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    onSystemSettingSubmit() {
      console.log('submit')
    }
  }
}
</script>

<style>
.protocolSelect {
  width: 100px;
}
</style>
