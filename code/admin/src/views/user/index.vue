<template>
  <div class="bg">
    <div class="userContainer">
      <el-row :gutter="20">
        <el-col :span="8">
          <div class="userPanel">
            <img :src="form.imgUrl" class="avatar">
            <div class="info">
              <div class="userName">{{ form.username }}</div>
              <div class="introduction">{{ form.introduction }}</div>
              <div class="email">
                <i class="el-icon-message" />
                {{ form.email }}
              </div>
              <div class="site">
                <i class="el-icon-location-outline" />
                {{ form.site }}
              </div>
            </div>
          </div>
        </el-col>
        <el-col :span="16">
          <div class="setting">
            <el-form ref="form" :model="form">
              <el-form-item label="头像">
                <div>
                  <el-button title="请先在附件中上传图片">选择头像图片</el-button>
                </div>
              </el-form-item>
              <el-form-item label="用户名">
                <el-input v-model="form.username" />
              </el-form-item>
              <el-form-item label="简介">
                <el-input v-model="form.introduction" />
              </el-form-item>
              <el-form-item label="邮箱">
                <el-input v-model="form.email" />
              </el-form-item>
              <el-form-item label="个人网站">
                <el-input v-model="form.site" />
              </el-form-item>
              <el-form-item>
                <el-button type="primary" @click="onSubmit">保存</el-button>
              </el-form-item>
            </el-form>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        imgUrl:
          'https://wpimg.wallstcn.com/69a1c46c-eb1c-4b46-8bd4-e9e686ef5251.png',
        username: '白露',
        introduction: '个人博客巴拉巴拉巴拉吧',
        email: 'kuari@justmylife.cc',
        site: 'www.justmylife.cc'
      }
    }
  },
  methods: {
    onSubmit() {
      this.$message({
        type: 'success',
        message: '保存个人信息成功'
      })
    }
  }
}
</script>

<style scoped>
div.bg {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  background-size: 100% 100%;
  position: absolute;
  background-color: #f2f2f2;
}
div.userContainer {
  padding: 30px;
}
div.userPanel {
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
  padding: 30px;
  background-color: white;
  height: 400px;
  text-align: center;
}
.avatar {
  border-radius: 50%;
  margin-bottom: 50px;
  margin-top: 30px;
  height: 100px;
  width: 100px;
}
div.userName {
  font-size: 25px;
  font-weight: 500;
  margin-bottom: 10px;
}
div.introduction {
  color: #444343;
  margin-bottom: 40px;
}
div.site,
div.email {
  color: #444343;
  margin: 1px 0;
}
div.setting {
  padding: 0 20px;
}
</style>
