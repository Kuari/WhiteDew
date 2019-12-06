<template>
  <div class="recentArticlePanel">
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column label="最近文章">
        <template slot-scope="scope">
          <a href="#" target="_blank">
            <span>{{ scope.row.article | articleLength }}</span>
          </a>
        </template>
      </el-table-column>
      <el-table-column prop="clicknumber" label="点击数"></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          article: "明月几时有，把酒问青天。",
          clicknumber: 200
        },
        {
          article: "不知天上宫阙，今夕是何年。",
          clicknumber: 200
        },
        {
          article: "我欲乘风归去，惟恐琼楼玉宇，高处不胜寒。",
          clicknumber: 200
        },
        {
          article: "起舞弄清影，何似在人间！",
          clicknumber: 200
        },
        {
          article: "转朱阁，低绮户，照无眠。",
          clicknumber: 200
        },
        {
          article: "不应有恨，何事长向别时圆？",
          clicknumber: 200
        },
        {
          article: "人有悲欢离合，月有阴晴圆缺，此事古难全。",
          clicknumber: 200
        },
        {
          article: "但愿人长久，千里共婵娟。",
          clicknumber: 200
        }
      ]
    };
  },
  filters: {
    articleLength(article) {
      if (article.length > 10) return article.substring(0, 10) + "...";
      return article;
    }
  }
};
</script>

<style scoped>
div.recentArticlePanel {
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
  padding: 20px;
  background-color: white;
}
</style>