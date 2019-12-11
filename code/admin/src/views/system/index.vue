<template>
  <div class="bg">
    <div class="systemContainer">
      <div class="panel"><systemSetting /></div>
      <div class="panel"><mail /></div>
      <div class="panel"><footerinfo /></div>
    </div>
  </div>
</template>

<script>
import systemSetting from './components/systemSetting'
import mail from './components/mail'
import footerinfo from './components/footer'

export default {
  components: {
    systemSetting,
    mail,
    footerinfo
  }
}
</script>

<style scoped>
div.bg {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  background-color: #f2f2f2;
}
div.systemContainer {
  padding: 30px;
}
div.panel {
  margin: 20px;
}
</style>
