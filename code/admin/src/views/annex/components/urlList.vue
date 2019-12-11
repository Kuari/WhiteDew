<template>
  <div>
    <!-- 图片列表 -->
    <el-row :gutter="5">
      <el-col :span="6">
        <div v-for="(item, index) in column.column1" :key="index" class="imgContainer">
          <el-card :body-style="{ padding: '0px' }">
            <el-image :src="item.url" lazy fit="fill" class="elImage" />
            <div style="padding: 14px;">
              <div class="bottom clearfix">
                <time class="time">{{ item.time }}</time>
                <el-button type="text" class="button" @click="moreImageInfo(item)">详情</el-button>
              </div>
            </div>
          </el-card>
        </div>
      </el-col>
      <el-col :span="6">
        <div v-for="(item, index) in column.column2" :key="index" class="imgContainer">
          <el-card :body-style="{ padding: '0px' }">
            <el-image :src="item.url" lazy fit="fill" class="elImage" />
            <div style="padding: 14px;">
              <div class="bottom clearfix">
                <time class="time">{{ item.time }}</time>
                <el-button type="text" class="button" @click="moreImageInfo(item)">详情</el-button>
              </div>
            </div>
          </el-card>
        </div>
      </el-col>
      <el-col :span="6">
        <div v-for="(item, index) in column.column3" :key="index" class="imgContainer">
          <el-card :body-style="{ padding: '0px' }">
            <el-image :src="item.url" lazy fit="fill" class="elImage" />
            <div style="padding: 14px;">
              <div class="bottom clearfix">
                <time class="time">{{ item.time }}</time>
                <el-button type="text" class="button" @click="moreImageInfo(item)">详情</el-button>
              </div>
            </div>
          </el-card>
        </div>
      </el-col>
      <el-col :span="6">
        <div v-for="(item, index) in column.column4" :key="index" class="imgContainer">
          <el-card :body-style="{ padding: '0px' }">
            <el-image :src="item.url" lazy fit="fill" class="elImage" />
            <div style="padding: 14px;">
              <div class="bottom clearfix">
                <time class="time">{{ item.time }}</time>
                <el-button type="text" class="button" @click="moreImageInfo(item)">详情</el-button>
              </div>
            </div>
          </el-card>
        </div>
      </el-col>
    </el-row>
    <!-- 图片列表 结束 -->

    <!-- 分页 -->
    <div class="footer">
      <el-pagination
        background
        layout="prev, pager, next"
        :page-size="pagesize"
        :total="urls.length"
        @current-change="changeCurrent"
      />
    </div>
    <!-- 分页 结束 -->

    <imageInfo :dialog="dialog" :form="imageInfoForm" @dialogchange="dialogchange" />
  </div>
</template>

<script>
import imageInfo from './imgeInfo'

export default {
  components: {
    imageInfo
  },
  props: {
    urls: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  data() {
    return {
      column: {
        column1: [],
        column2: [],
        column3: [],
        column4: []
      },
      pagesize: 20,
      currentPage: 1,
      dialog: false,
      imageInfoForm: {}
    }
  },
  computed: {
    imageShowData() {
      return this.urls.slice(
        (this.currentPage - 1) * this.pagesize,
        this.currentPage * this.pagesize
      )
    }
  },
  created() {
    this.intiUrls()
  },
  methods: {
    intiUrls() {
      this.column.column1 = []
      this.column.column2 = []
      this.column.column3 = []
      this.column.column4 = []
      let n = 1
      this.imageShowData.forEach(item => {
        this.column[`column${n}`].push(item)
        n < 4 ? n += 1 : n = 1
      })
    },
    moreImageInfo(imageInfo) {
      this.imageInfoForm = imageInfo
      this.dialog = true
    },
    changeCurrent(current) {
      this.currentPage = current
      this.intiUrls()
    },
    dialogchange(val) {
      this.dialog = val
    }
  }
}
</script>

<style scoped>
.imgContainer {
  padding: 10px;
  overflow: auto;
}

.elImage {
  width: 100%;
}
.time,
.botton {
  font-size: 12px;
}
div.footer {
  text-align: right;
}
</style>
