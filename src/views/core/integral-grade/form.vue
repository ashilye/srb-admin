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
  methods: {
    // 保存或更新
    saveOrUpdate() {
      this.saveBtnDisabled = true
      // 新增
      this.saveData()
      // 更新
      this.updateData()
    },
    saveData() {
      integralGradeApi.save(this.integralGrade).then(response => {
        this.$message({
          type: 'success',
          message: response.message
        })
      })
    },
    updateData() {

    }
  }
}
</script>

<style scoped>

</style>
