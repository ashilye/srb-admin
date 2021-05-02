<template>
  <div class="app-container">
    <!--表格-->
    <el-table :data="list" border stripe>
      <el-table-column type="index" width="50"/>
      <el-table-column prop="borrowAmount" label="借款额度"/>
      <el-table-column prop="integralStart" label="积分区间开始"/>
      <el-table-column prop="integralEnd" label="积分区间结束"/>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button type="danger" size="mini" icon="el-icon-delete" @click="removeById(scope.row.id)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import integralGradeApi from '@/api/core/integral-grade'
export default {
  name: 'List',
  data() {
    return {
      list: []
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      integralGradeApi.list().then(response => {
        this.list = response.data.list
      })
    },
    removeById(id) {
      console.log('id', id)
      const _that = this
      // debugger
      this.$confirm('此操作将永久删除该记录, 是否继续?', '提示', {
        confirmButtonText: '删除',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        integralGradeApi.removeById(id).then(response => {
          _that.$message({
            showClose: true,
            message: response.message,
            type: 'success'
          })
          // 删除成功后 刷新页面
          _that.fetchData()
        })
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消删除'
        })
      })
    }
  }
}
</script>

<style scoped>

</style>
