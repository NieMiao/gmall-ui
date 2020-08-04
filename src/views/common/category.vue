<template>
  <el-tree
    :data="dataList"
    :props="defaultProps"
    node-key="catId"
    @node-click="nodeClick">
  </el-tree>
</template>

<script>
  export default {
    data() {
      return {
        dataList: [],
        defaultProps: {
          children: 'children',
          label: 'name'
        }
      }
    },
    methods: {
      getDataList() {
        this.$http({
          url: this.$http.adornUrl('/product/category/tree'),
          method: 'get'
        }).then(({data}) => {
          if (data.success) {
            this.dataList = data.data
          } else {
            this.dataList = []
          }
        })
      },
      nodeClick(data) {
        console.log("子组件category的节点被点击", data);
        this.$emit("tree-node-click",data);
      }
    },
    created() {
      this.getDataList();
    }
  }
</script>

<style scoped>

</style>
