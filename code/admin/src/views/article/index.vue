<template>
  <div class="container">
    <div class="optionTool">
      <el-button type="primary" icon="el-icon-edit">写文章</el-button>
      <el-button
        type="danger"
        icon="el-icon-delete"
        :disabled="deleteArticleBtn"
        @click="deleteArticle"
      >删除({{ multipleSelection.length }})</el-button>
    </div>
    <el-table
      ref="multipleTable"
      :data="separateLists"
      tooltip-effect="dark"
      style="width: 100%"
      @selection-change="handleSelectionChange"
    >
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column label="文章名" width="250">
        <template slot-scope="scope">{{ scope.row.article | articleNameLength }}</template>
      </el-table-column>
      <el-table-column label="状态" width="80">
        <template slot-scope="scope">
          <el-tag
            :type="scope.row.status | transArticleStatusTag"
          >{{ scope.row.status | transArticleStatus }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column label="分类" width="80">
        <template slot-scope="scope">
          <el-tag>{{ scope.row.classification }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column prop="tag" label="标签" width="250">
        <template slot-scope="scope">
          <el-tag
            v-for="(item, index) in scope.row.tag.slice(0, 3)"
            :key="index"
            class="tag"
          >{{ item }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column prop="click" label="点击" width="50"></el-table-column>
      <el-table-column prop="comment" label="评论" width="50"></el-table-column>
      <el-table-column prop="time" label="时间" width="200"></el-table-column>
      <el-table-column fixed="right" label="操作" width="200">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
          <el-button size="mini" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <div class="footer">
      <el-pagination
        background
        layout="prev, pager, next"
        :page-size="pagesize"
        :total="lists.length"
        @current-change="changeCurrent"
      ></el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lists: [
        {
          article: "1明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "2明月几时有，把酒问青天",
          status: 0,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "3明月几时有，把酒问青天",
          status: 0,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "4明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "5明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "6明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "7明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "8明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "9明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "10明月几时有，把酒问青天",
          status: 0,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "11明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "12明月几时有，把酒问青天",
          status: 0,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "13明月几时有，把酒问青天",
          status: 0,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "14明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "15明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "16明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "17明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "18明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "19明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "20明月几时有，把酒问青天",
          status: 0,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "21明月几时有，把酒问青天",
          status: 1,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "22明月几时有，把酒问青天",
          status: 0,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        },
        {
          article: "23明月几时有，把酒问青天",
          status: 0,
          classification: "宋词",
          tag: ["宋词", "苏轼", "明月"],
          click: 300,
          comment: 200,
          time: "2019-12-6 10:00"
        }
      ],
      multipleSelection: [],
      pagesize: 10,
      currentPage: 1
    };
  },

  methods: {
    toggleSelection(rows) {
      if (rows) {
        rows.forEach(row => {
          this.$refs.multipleTable.toggleRowSelection(row);
        });
      } else {
        this.$refs.multipleTable.clearSelection();
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val;
    },
    handleEdit(val) {
      // 编辑文章，跳转到编辑页面
      console.log("编辑");
    },
    handleDelete(val) {
      // 单个删除
      this.lists.splice(val, 1);
    },
    deleteArticle() {
      this.$confirm("此操作将删除该文件, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
          // 删除文件
          for (let i = 0; i < this.lists.length; i++) {
            if (this.multipleSelection.indexOf(this.lists[i]) > -1) {
              this.lists.splice(i, 1);
              i -= 1;
            }
          }
          this.$message({
            type: "success",
            message: "删除成功!"
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除"
          });
        });
    },
    changeCurrent(current) {
      this.currentPage = current;
    }
  },
  filters: {
    transArticleStatus(status) {
      // 转换文章状态 0-未发布 1-已经发布
      switch (status) {
        case 0:
          return "未发布";
        case 1:
          return "已发布";
      }
    },
    transArticleStatusTag(status) {
      // 转换文章状态的标签 0-未发布 1-已经发布 2-回收站
      switch (status) {
        case 0:
          return "info";
        case 1:
          return "success";
      }
    },
    articleNameLength(article) {
      // 文章名长度限制，限制为10
      if (article.length > 15) return article.substring(0, 15) + "...";
      return article;
    }
  },
  computed: {
    deleteArticleBtn() {
      // 删除按钮的禁用状态，未选中时为禁止状态
      if (this.multipleSelection.length != 0) {
        return false;
      }
      return true;
    },
    separateLists() {
      // 分页后的列表，直接在html里面写表达式导致无法选中的bug
      return this.lists.slice(
        (this.currentPage - 1) * this.pagesize,
        this.currentPage * this.pagesize
      );
    }
  },
  created() {
    this.total = this.lists.length;
  }
};
</script>

<style scoped>
.tag {
  margin-right: 2px;
}
div.optionTool {
  margin: 20px 0;
}
.footer {
  text-align: right;
  margin-top: 20px;
}
</style>