<template>
  <ve-pie :data="chartData" :settings="chartSettings" />
</template>

<script>
export default {
  data() {
    this.chartSettings = {
      roseType: 'radius'
    }
    return {
      chartData: {
        columns: ['浏览器', '访问数量'],
        rows: [
          { 浏览器: 'Chrome', 访问数量: 3903 },
          { 浏览器: 'Firefox', 访问数量: 3530 },
          { 浏览器: 'Safari', 访问数量: 2923 },
          { 浏览器: 'IE', 访问数量: 1723 }
        ]
      }
    }
  }
}
</script>
