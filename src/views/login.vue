
<template>
  <div class="login">
    <canva></canva>
    <el-card class="box-card" shadow>
      <el-form
        :model="ruleForm"
        :rules="rules"
        ref="ruleForm"
        label-width="100px"
        class="demo-ruleForm">
        <el-form-item label="用户名" prop="name">
          <el-input v-model="ruleForm.name"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="desc">
          <el-input v-model="ruleForm.desc" show-password></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')" >登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
import canva from "../components/canvas.vue";
export default {
  components: { canva },
  data() {
    return {
      ruleForm: {
        name: "",
        desc: "",
      },
      rules: {
        name: [
          { required: true, message: "请输入用户名", trigger: "blur" },
          {
            min: 3,
            max: 5,
            message: "长度在 3 到 5 个字符",
            trigger: "blur",
          },
        ],
        desc: [{ required: true, message: "请输入密码", trigger: "blur" },  {
            min:6,
            max:10,
            message: "长度在6 到 10 个字符",
            trigger: "blur",
          },],
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          // alert("submit!");
          this.$router.push({path:'/home'})
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
  },
};
</script>

<style scoped>
.login {
  width: 100%;
  height: 800px;
  position: relative;
  /* color: #fff; */
}
.box-card {
  width: 500px;
  height: 200px;
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  top: 8rem;
  margin: auto;
  z-index: 999;
  border-radius: 10px;
  /* background: linear-gradient(#1a237e, #5761cc, #838cee);  渐变色*/
}
</style>
