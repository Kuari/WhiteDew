<template>
  <div class="container">
    <el-row :gutter="10">
      <el-col :span="8">
        <!-- 文件上传 -->
        <div class="fixed">
          <el-upload
            drag
            action="/"
            multiple
            list-type="picture"
            :file-list="fileList"
            :on-success="handleUploadSuccess"
            :before-upload="beforeUpload"
          >
            <i class="el-icon-upload" />
            <div class="el-upload__text">
              将文件拖到此处，或
              <em>点击上传</em>
            </div>
            <div slot="tip" class="el-upload__tip">只能上传jpg/png文件</div>
          </el-upload>
        </div>
      </el-col>
      <el-col :span="16">
        <!-- 图片列表 -->
        <div class="imageListContainer">
          <urlList :urls="urls" />
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import urlList from './components/urlList'

export default {
  components: {
    urlList
  },
  data() {
    return {
      fileList: [],
      urls: [
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10MB',
          mdurl: 'mdurl'

        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/0/6f/e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/9/bb/e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10MB',
          mdurl: 'mdurl'

        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/0/6f/e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/9/bb/e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10MB',
          mdurl: 'mdurl'

        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/0/6f/e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/9/bb/e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10MB',
          mdurl: 'mdurl'

        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/0/6f/e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/9/bb/e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10MB',
          mdurl: 'mdurl'

        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/0/6f/e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/9/bb/e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10MB',
          mdurl: 'mdurl'

        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/0/6f/e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/9/bb/e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10MB',
          mdurl: 'mdurl'

        },
        {
          name: '3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/0/6f/e35ff375812e6b0020b6b4e8f9583jpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        },
        {
          name: 'e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          url: 'https://fuss10.elemecdn.com/9/bb/e27858e973f5d7d3904835f46abbdjpeg.jpeg',
          time: '2019-12-11 13:00',
          size: '10kb',
          mdurl: 'mdurl'
        }
      ]
    }
  },
  methods: {
    beforeUpload(file) {
      const isJPG = file.type === 'image/jpeg'

      if (!isJPG) {
        this.$message.error('上传头像图片只能是 JPG 格式!')
      }
      return isJPG
    },
    handleUploadSuccess() {
      console.log('success')
    },
    handleUrlList() {
      this.urlList.forEach()
    }
  }
}
</script>

<style scoped>
div.imageListContainer {
  border: none;
  border-left: 1px solid #DCDFE6;
  padding: 10px;
}
</style>
