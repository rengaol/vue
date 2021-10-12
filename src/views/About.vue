<template>
  <div class="about">
    <div class="content">
      <div class="box">
        <div class="left">
          <el-steps :space="200" :active="2" finish-status="success">
            <el-step title="已完成"></el-step>
            <el-step title="进行中"></el-step>
            <el-step title="步骤 3"></el-step>
          </el-steps>
        </div>
        <div class="right">rgiht</div>
      </div>
    </div>
  </div>
</template>
<script>
export default {};
</script>
<style scoped>
.box {
  display: flex;
  align-content: space-around;
  flex-direction: row;
}
.left {
  flex: 1;
  border: 1px solid #000;
}
.right {
  flex: 1;
  border: 1px solid rebeccapurple;
}
</style>
