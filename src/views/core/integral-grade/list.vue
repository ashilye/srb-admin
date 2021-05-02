<template>
  <div class="app-container">
    <!--表格-->
    <el-table :data="list" border stripe>
      <el-table-column type="index" width="50"/>
      <el-table-column prop="borrowAmount" label="借款额度"/>
      <el-table-column prop="integralStart" label="积分区间开始"/>
      <el-table-column prop="integralEnd" label="积分区间结束"/>
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
    }
  }
}
</script>

<style scoped>

</style>
