<template>
  <div>
    heihei
  </div>
</template>

<script>
export default {
  props: {
    urlList: {
      type: Array
    }
  },
  data() {
    return {
      column: {
        column1: [],
        column2: [],
        column3: [],
        column4: []
      }
    }
  },
  created() {
    this.intiUrlList()
  },
  methods: {
    intiUrlList() {
      let n = 1
      this.urlList.forEach(item => {
        this.column[`column${n}`].push(item)
        n < 4 ? n += 1 : n = 0
      })
      console.log(this.column)
    }
  }
}
</script>
