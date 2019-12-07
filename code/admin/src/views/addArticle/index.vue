<template>
  <div class="container">
    <el-form ref="ruleForm" :model="form" label-width="80px" :rules="rules">

      <span v-show="headerStatus">

        <el-form-item label="文章名" prop="title" required>
          <el-input v-model="form.title" />
        </el-form-item>

        <el-form-item label="副标题" prop="subtitle" label-width="80px" required>
          <el-input v-model="form.subtitle" />
        </el-form-item>

        <el-row>
          <el-col :span="8">
            <el-form-item label="发布时间" prop="time" required>
              <el-date-picker
                v-model="form.time"
                type="datetime"
                placeholder="选择发布时间"
                align="right"
                :picker-options="pickerOptions"
              />
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="允许评论">
              <el-switch v-model="form.comment" />
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="列表图片">
              <el-button>选择图片</el-button>
            </el-form-item>
          </el-col>
        </el-row>

      </span>

      <el-form-item>
        <el-row>
          <el-col :span="16">
            <el-button type="primary" @click="onSubmit('ruleForm')">发布</el-button>
            <el-button type="info" @click="onSave('ruleForm')">保存为草稿</el-button>
          </el-col>
          <el-col :span="8">
            <div class="hideHeader" @click="headerStatus = !headerStatus">
              <i :class="headerStatus ? 'el-icon-arrow-up':'el-icon-arrow-down'" />
              {{ headerStatus? '收起' : '展开' }}
            </div>
          </el-col>
        </el-row>
      </el-form-item>

    </el-form>

    <!-- 富文本编辑器 -->
    <div class="markdownEdit">
      <el-row :gutter="20">
        <el-col :span="12">
          <el-input
            v-model="input"
            type="textarea"
            :rows="50"
            placeholder="请使用markdown语法编写~"
          />
        </el-col>
        <el-col :span="12">
          <vue-markdown :source="input" />
        </el-col>
      </el-row>
    </div>
    <!-- 富文本编辑器 结束 -->

  </div>
</template>

<script>
import VueMarkdown from 'vue-markdown'
import Prism from 'prismjs'
import '../../../node_modules/prismjs/themes/prism.css'

export default {
  components: {
    VueMarkdown
  },
  data() {
    return {
      input: '### 请使用markdown语法编写~ 8-)',
      headerStatus: true,
      form: {
        title: '',
        subtitle: '',
        time: '',
        comment: true
      },
      rules: {
        title: [
          { required: true, message: '请输入文章名', trigger: 'blur' }
        ],
        subtitle: [
          { required: true, message: '请输入简介', trigger: 'blur' }
        ],
        time: [
          { type: 'date', required: true, message: '请选择发布时间', trigger: 'change' }
        ]
      },
      pickerOptions: {
        shortcuts: [{
          text: '今天',
          onClick(picker) {
            picker.$emit('pick', new Date())
          }
        }, {
          text: '昨天',
          onClick(picker) {
            const date = new Date()
            date.setTime(date.getTime() - 3600 * 1000 * 24)
            picker.$emit('pick', date)
          }
        }, {
          text: '一周前',
          onClick(picker) {
            const date = new Date()
            date.setTime(date.getTime() - 3600 * 1000 * 24 * 7)
            picker.$emit('pick', date)
          }
        }]
      }
    }
  },
  updated() {
    Prism.highlightAll()
  },
  methods: {
    onSubmit(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    onSave(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('save!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>

<style scoped>
div.markdownEdit {
  margin: 30px 10px;
}
div.hideHeader {
  text-align: right;
  margin-right: 20px;
}
</style>
