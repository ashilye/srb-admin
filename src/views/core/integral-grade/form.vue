<template>
  <div class="app-container">
    <!-- 输入表单-->
    <el-form label-width="120px">
      <el-form-item label="借款额度">
        <el-input-number v-model="integralGrade.borrowAmount" :min="0" />
      </el-form-item>
      <el-form-item label="积分区间开始">
        <el-input-number v-model="integralGrade.integralStart" :min="0" />
      </el-form-item>
      <el-form-item label="积分区间结束">
        <el-input-number v-model="integralGrade.integralEnd" :min="0" />
      </el-form-item>
      <el-form-item>
        <el-button
          :disabled="saveBtnDisabled"
          type="primary"
          @click="saveOrUpdate"
        >
          保存
        </el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
// 引入api模块
import integralGradeApi from '@/api/core/integral-grade'
export default {
  name: 'Form',
  data() {
    return {
      saveBtnDisabled: false, // 是否禁用保存按钮，防止表单重复提交
      integralGrade: {}
    }
  },
  created() {
    // 当路由中存在id时 就是回显表单
    if (this.$route.params.id) {
      this.fetchById(this.$route.params.id)
    }
  },
  methods: {
    fetchById(id) {
      integralGradeApi.getById(id).then(response => {
        this.integralGrade = response.data.record
      })
    },
    // 保存或更新
    saveOrUpdate() {
      this.saveBtnDisabled = true
      if (this.$route.params.id) {
        // 更新
        this.updateData()
      } else {
        // 新增
        this.saveData()
      }
    },
    saveData() {
      integralGradeApi.save(this.integralGrade).then(response => {
        this.$message({
          type: 'success',
          message: response.message
        })
      })
      // 保存成功后 进行路由跳转
      this.$router.push('/core/integral-grade/list')
    },
    updateData() {
      integralGradeApi.updateById(this.integralGrade).then(response => {
        this.$message({
          type: 'success',
          message: response.message
        })
      })
      // 更新成功后 进行路由跳转
      this.$router.push('/core/integral-grade/list')
    }
  }
}
</script>

<style scoped>

</style>
