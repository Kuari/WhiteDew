<template>
  <div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>邮箱设置</span>
        <el-switch
          v-model="openMail"
          style="float: right; padding: 3px 0"
        />
      </div>
      <div class="text">
        heihei
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      openMail: true
    }
  }
}
</script>

<style scoped>

</style>
