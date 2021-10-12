<template>
<!-- 表格 -->
  <el-container style="border: 1px solid #eee">
    <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
      <navs/> <!--侧边栏  -->
      
    </el-aside>
    <el-container>
      <el-header style="text-align: right; font-size: 12px">
      <menus/>  <!-- 头部导航栏  -->
      </el-header>
      <el-main>
        <el-table :data="tableData" height="500px">
          <el-table-column prop="date" label="日期" width="140">
          </el-table-column>
          <el-table-column prop="name" label="姓名" width="120">
          </el-table-column>
          <el-table-column prop="address" label="地址"> </el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import menus from "@/components/menu.vue";
import navs from "@/components/nav.vue";

export default {
  components: { menus, navs },
  data() {
    const item = {
      date: "2016-05-02",
      name: "王小虎",
      address: "上海市普陀区金沙江路 1518 弄",
    };
    return {
      tableData: Array(15).fill(item),
    };
  },
  mounted(){
        console.log('this.talbe')
  }
};
</script>

<style scoped>
.el-header {
  color: var(--el-text-color-primary);
  margin-left: -20px;
  line-height: 60px;
}

.el-aside {
  color: var(--el-text-color-primary);
}
</style>
