<template>
  <div class="container">
    <div class="panel"><systemSetting /></div>
    <div class="panel"><mail /></div>
  </div>
</template>

<script>
import systemSetting from './components/systemSetting'
import mail from './components/mail'

export default {
  components: {
    systemSetting,
    mail
  }
}
</script>

<style scoped>
div.panel {
  margin: 20px;
}
</style>
