<template>
  <div>
    <el-drawer
      ref="drawer"
      title="图片详情"
      :visible.sync="localDialog"
      :before-close="cancelForm"
      direction="rtl"
      custom-class="drawer"
    >
      <div class="drawer__content">
        <el-form :model="form">
          <el-form-item label="图片名" :label-width="formLabelWidth">
            <el-input v-model="localForm.name" />
          </el-form-item>
          <el-form-item label="上传时间" :label-width="formLabelWidth">
            <el-input v-model="localForm.time" />
          </el-form-item>
          <el-form-item label="文件大小" :label-width="formLabelWidth">
            <el-input v-model="localForm.size" />
          </el-form-item>
          <el-form-item label="图片地址" :label-width="formLabelWidth">
            <el-input v-model="localForm.url">
              <el-button slot="prepend" class="copyImageUrl" icon="el-icon-document-copy" :data-clipboard-text="localForm.url" @click="copyUrl('.copyImageUrl')" />
            </el-input>
          </el-form-item>
          <el-form-item label="MD代码" :label-width="formLabelWidth">
            <el-input v-model="localForm.mdurl">
              <el-button slot="prepend" icon="el-icon-document-copy" class="copyMdUrl" :data-clipboard-text="localForm.mdurl" @click="copyUrl('.copyMdUrl')" />
            </el-input>
          </el-form-item>
        </el-form>
        <div class="drawerFooter">
          <el-button type="danger" :loading="loading" @click="$refs.drawer.closeDrawer()">{{ loading ? '删除中 ...' : '删 除' }}</el-button>
          <el-button @click="cancelForm">关闭</el-button>
        </div>
      </div>
    </el-drawer>
  </div>
</template>

<script>
import Clipboard from 'clipboard'

export default {
  props: {
    dialog: {
      type: Boolean,
      default: false
    },
    form: {
      type: Object,
      default: () => {
        return {
          name: 'test.jpg',
          size: '5MB',
          url: 'imageUrl',
          mdurl: 'markdownUrl'
        }
      }
    }
  },
  data() {
    return {
      loading: false,
      formLabelWidth: '80px',
      localDialog: this.dialog,
      localForm: this.form
    }
  },
  watch: {
    dialog(val) {
      this.localDialog = val
    },
    form(val) {
      this.localForm = val
    }
  },
  methods: {
    handleClose(done) {
      if (this.loading) {
        return
      }
      this.$confirm('确定要提交表单吗？')
        .then(_ => {
          this.loading = true
          this.timer = setTimeout(() => {
            done()
            // 动画关闭需要一定的时间
            setTimeout(() => {
              this.loading = false
            }, 400)
          }, 2000)
        })
        .catch(_ => {})
    },
    cancelForm() {
      this.loading = false
      this.localDialog = false
      this.$emit('dialogchange', this.localDialog)
    },
    copyUrl(val) {
      var clipboard = new Clipboard(val)
      clipboard.on('success', e => {
        this.$message({
          message: '复制图片地址成功',
          type: 'success'
        })
        clipboard.destroy()
      })
      clipboard.on('error', e => {
        this.$message({
          message: '抱歉，该浏览器不支持复制',
          type: 'danger'
        })
        clipboard.destroy()
      })
    }
  }
}
</script>

<style scoped>
.drawerFooter {
    margin-left: 30px;
}
</style>
