<template>
  <ve-histogram :data="chartData" :settings="chartSettings" />
</template>

<script>
export default {
  data() {
    this.chartSettings = {
      metrics: ['评论数量'],
      dimension: ['日期']
    }
    return {
      chartData: {
        columns: ['日期', '评论数量'],
        rows: [
          { 日期: '12/1', 评论数量: 1393 },
          { 日期: '12/2', 评论数量: 3530 },
          { 日期: '12/3', 评论数量: 2923 },
          { 日期: '12/4', 评论数量: 1723 },
          { 日期: '12/5', 评论数量: 3792 },
          { 日期: '12/6', 评论数量: 4593 }
        ]
      }
    }
  }
}
</script>
