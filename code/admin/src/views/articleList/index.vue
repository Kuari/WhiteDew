<template>
  <div class="container">
    <div class="optionTool">
      <el-row>
        <el-col :span="12">
          <div class="buttonGroup">
            <el-button type="primary" icon="el-icon-edit">写文章</el-button>
            <el-button
              type="danger"
              icon="el-icon-delete"
              :disabled="deleteArticleBtn"
              @click="deleteArticle"
            >删除({{ multipleSelection.length }})</el-button>
          </div>
        </el-col>
        <el-col :span="12">
          <div class="searchInput"><el-input v-model="search" placeholder="搜索" /></div>
        </el-col>
      </el-row>
    </div>
    <el-table
      ref="multipleTable"
      :data="tableData"
      tooltip-effect="dark"
      style="width: 100%"
      @selection-change="handleSelectionChange"
    >
      <el-table-column type="selection" width="55" />
      <el-table-column label="文章名" width="400" sortable>
        <template slot-scope="scope">{{ scope.row.article.length > 20? scope.row.article.substring(0, 20) + '...' : scope.row.article }}</template>
      </el-table-column>
      <el-table-column label="状态" width="80" sortable>
        <template slot-scope="scope">
          <el-tag
            :type="scope.row.status? 'success' : 'info'"
          >{{ scope.row.status? '已发布' : '未发布' }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column
        prop="classification"
        label="分类"
        column-key="classification"
        :filters="classificationList"
        :filter-method="tableFilterHandler"
      />
      <el-table-column prop="click" label="点击" />
      <el-table-column prop="comment" label="评论" />
      <el-table-column prop="time" label="时间" width="200" sortable />
      <el-table-column fixed="right" label="操作" width="200">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
          <el-button size="mini" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <div v-show="!search" class="footer">
      <el-pagination
        background
        layout="prev, pager, next"
        :page-size="pagesize"
        :total="lists.length"
        @current-change="changeCurrent"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lists: [
        {
          article: '1明月几时有，把酒问青天',
          status: 1,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '2明月几时有，把酒问青天',
          status: 0,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '3明月几时有，把酒问青天',
          status: 0,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '4明月几时有，把酒问青天',
          status: 1,
          classification: '宋词3',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '5明月几时有，把酒问青天',
          status: 1,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '6明月几时有，把酒问青天',
          status: 1,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '7明月几时有，把酒问青天',
          status: 1,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '8明月几时有，把酒问青天',
          status: 1,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '9明月几时有，把酒问青天',
          status: 1,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '10明月几时有，把酒问青天',
          status: 0,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '11明月几时有，把酒问青天',
          status: 1,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '12明月几时有，把酒问青天',
          status: 0,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '13明月几时有，把酒问青天',
          status: 0,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '14明月几时有，把酒问青天',
          status: 1,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '15明月几时有，把酒问青天',
          status: 1,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '16明月几时有，把酒问青天',
          status: 1,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '17明月几时有，把酒问青天',
          status: 1,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '18明月几时有，把酒问青天',
          status: 1,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '19明月几时有，把酒问青天',
          status: 1,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '20明月几时有，把酒问青天',
          status: 0,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '21明月几时有，把酒问青天',
          status: 1,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '22明月几时有，把酒问青天',
          status: 0,
          classification: '宋词1',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        },
        {
          article: '23明月几时有，把酒问青天',
          status: 0,
          classification: '宋词2',
          click: 300,
          comment: 200,
          time: '2019-12-6 10:00'
        }
      ],
      multipleSelection: [],
      classificationList: [],
      pagesize: 10,
      currentPage: 1,
      search: ''
    }
  },
  computed: {
    deleteArticleBtn() {
      // 删除按钮的禁用状态，未选中时为禁止状态
      if (this.multipleSelection.length !== 0) {
        return false
      }
      return true
    },
    tableData() {
      const search = this.search
      if (search) {
        return this.lists.filter(data => {
          return Object.keys(data).some(key => {
            return String(data[key]).toLowerCase().indexOf(search) > -1
          })
        })
      }
      return this.lists.slice(
        (this.currentPage - 1) * this.pagesize,
        this.currentPage * this.pagesize
      )
    }
  },
  created() {
    this.total = this.lists.length
    this.fetchData()
  },

  methods: {
    fetchData() {
      const beforeClassificationList = []
      this.lists.forEach(item => {
        if (beforeClassificationList.indexOf(item.classification) === -1) {
          beforeClassificationList.push(item.classification)
        }
      })
      beforeClassificationList.forEach(item => {
        this.classificationList.push({
          text: item,
          value: item
        })
      })
    },
    toggleSelection(rows) {
      if (rows) {
        rows.forEach(row => {
          this.$refs.multipleTable.toggleRowSelection(row)
        })
      } else {
        this.$refs.multipleTable.clearSelection()
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    handleEdit(val) {
      // 编辑文章，跳转到编辑页面
      console.log('编辑')
    },
    handleDelete(val) {
      // 单个删除
      this.lists.splice(val, 1)
    },
    deleteArticle() {
      this.$confirm('此操作将删除选中文章, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          // 删除文件
          for (let i = 0; i < this.lists.length; i++) {
            if (this.multipleSelection.indexOf(this.lists[i]) > -1) {
              this.lists.splice(i, 1)
              i -= 1
            }
          }
          this.$message({
            type: 'success',
            message: '删除成功!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          })
        })
    },
    changeCurrent(current) {
      this.currentPage = current
    },
    tableFilterHandler(value, row, column) {
      const property = column['property']
      return row[property] === value
    }
  }
}
</script>

<style scoped>
div.optionTool {
  margin: 20px 0;
}
.footer {
  text-align: right;
  margin-top: 20px;
}
</style>
