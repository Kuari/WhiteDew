<template>
  <div class="recentcommentPanel">
    <el-table :data="tableData" style="width: 100%">
      <el-table-column label="最新评论">
        <template slot-scope="scope">
          <a href="#" target="_blank">
            <span>{{ scope.row.comment | commentLength }}</span>
          </a>
        </template>
      </el-table-column>
      <el-table-column prop="username" label="用户名" align="right"></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          comment: "明月几时有，把酒问青天。",
          username: "Kuari"
        },
        {
          comment: "不知天上宫阙，今夕是何年。",
          username: "Kuari"
        },
        {
          comment: "我欲乘风归去，惟恐琼楼玉宇，高处不胜寒。",
          username: "Kuari"
        },
        {
          comment: "起舞弄清影，何似在人间！",
          username: "Kuari"
        },
        {
          comment: "转朱阁，低绮户，照无眠。",
          username: "Kuari"
        },
        {
          comment: "不应有恨，何事长向别时圆？",
          username: "Kuari"
        },
        {
          comment: "人有悲欢离合，月有阴晴圆缺，此事古难全。",
          username: "Kuari"
        },
        {
          comment: "但愿人长久，千里共婵娟。",
          username: "Kuari"
        }
      ]
    };
  },
  filters: {
    commentLength(comment) {
      if (comment.length > 6) return comment.substring(0, 6) + "...";
      return comment;
    }
  }
};
</script>

<style scoped>
div.recentcommentPanel {
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
  padding: 20px;
  background-color: white;
}
</style>