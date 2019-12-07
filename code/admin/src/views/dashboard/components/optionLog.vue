<template>
  <div class="logPanel">
    <el-table :data="lists" style="width: 100%">
      <el-table-column label="操作记录" fit="true">
        <template slot-scope="scope">
          <a href="#" target="_blank">
            <span>{{ scope.row.option | optionLength }}</span>
          </a>
        </template>
      </el-table-column>
      <el-table-column prop="time" label="时间" align="right" />
    </el-table>
  </div>
</template>

<script>
export default {
  filters: {
    optionLength(option) {
      if (option.length > 10) return option.substring(0, 10) + '...'
      return option
    }
  },
  data() {
    return {
      lists: [
        {
          option: '删除文章',
          time: '10:00'
        },
        {
          option: '删除页面',
          time: '10:00'
        },
        {
          option: '新增文章',
          time: '10:00'
        },
        {
          option: '新增文章',
          time: '10:00'
        },
        {
          option: '删除文章',
          time: '10:00'
        },
        {
          option: '删除文章',
          time: '10:00'
        },
        {
          option: '删除文章',
          time: '10:00'
        },
        {
          option: '删除文章',
          time: '10:00'
        },
        {
          option: '删除文章',
          time: '10:00'
        },
        {
          option: '删除文章',
          time: '10:00'
        }
      ]
    }
  }
}
</script>

<style scoped>
div.logPanel {
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
  padding: 20px;
  background-color: white;
}
</style>
