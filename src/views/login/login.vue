<template>
  <div class="login-bgd">
    <div class="login-box">
      <h1>管理平台</h1>
      <el-form
        :model="ruleForm"
        status-icon
        :rules="rules"
        ref="ruleForm"
        label-width="100px"
        class="demo-ruleForm"
      >
        <el-form-item label="用户名" prop="username">
          <el-input
            type="text"
            :model="ruleForm.username"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        
        <el-form-item :label="'密\xa0\xa0\xa0码'" prop="password">
          <el-input

          
            type="password"
            :model="ruleForm.password"
            :show-password="true"
          ></el-input>
        </el-form-item>
        <el-form-item label="验证码" prop="verificationCode">
          <div class="verificationCode-box">
            <el-input
              type="password"
              :model="ruleForm.verificationCode"
              autocomplete="off"
            ></el-input>
            <img height="40px" src="https://img1.baidu.com/it/u=4008228978,2338436789&fm=253&fmt=auto&app=138&f=PNG?w=232&h=139" alt="">
          </div>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')"
            >登录</el-button
          >
        </el-form-item>
      </el-form> 
     
    </div>
  </div>
</template>
<script>
export default {
  name: "login",
  data() {
    var validatorUsername =(_rule, value, callback) => {
      let _reg = /\w{4,12}/; //请求输入4-12为数字字母下划线
      if (value === "") {
       return callback(new Error("用户名不能为空"));
      }  else {
      return callback();
      }
    };
    var validatePassword =(_rule,value,callback)=>{
      let reg = /\w{6,}/;
      if (value === '') {
        callback(new Error("密码不能为空"))
      }else if(!reg.test(value)){
        callback(new Error("请输入至少6位密码"))
      }else{
        callback()
      }
    }
  
    return {
      ruleForm: {
        username: "",
        password: "",
        verificationCode: "",
      },
      rules: {
        username: [
          { required: true, validator:validatorUsername, trigger: 'blur' },
        ],
        password: [
          { required: true, validator:validatePassword,trigger: "blur" },
        ],
        verificationCode: [
          { required: true, message: "验证码不能为空", trigger: "blur" },
        ],
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    

  },
};

</script>
<style lang="less" scoped>
.login-bgd {
  width: 100%;
  height: 100%;
  position: relative;
  background: url(../../assets/timg.png) center top no-repeat;
  .login-box {
    width: 400px;
    background-color: aliceblue;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 5%;
    padding-top: 20px;
    padding-right: 20px;
    h1 {
      text-align: center;
      margin-bottom: 20px;
      padding-top: 20px;
      font-size: 20px;
    }
    .verificationCode-box{
        display: flex;
        img{
            margin-left: 20px;
        }
    }
  }
}
</style>