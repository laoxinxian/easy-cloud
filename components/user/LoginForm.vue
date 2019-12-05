<template>
  <el-form
    ref="form"
    :model="form"
    :rules="rules"
    class="form"
  >
    <el-form-item class="form-item" prop="username">
      <el-input
        v-model="form.username"
        placeholder="用户名/手机"
      />
    </el-form-item>

    <el-form-item class="form-item" prop="password">
      <el-input
        v-model="form.password"
        placeholder="密码"
        type="password"
      />
    </el-form-item>

    <p class="form-text">
      <nuxt-link to="#">
        忘记密码
      </nuxt-link>
    </p>

    <el-button
      @click="handleLoginSubmit"
      class="submit"
      type="primary"
    >
      登录
    </el-button>
  </el-form>
</template>

<script>
export default {
  data () {
    return {
      // 表单数据
      form: {
        username: '13800138000',
        password: '123456'

      },
      // 表单规则
      rules: {
        username: [
          {
            required: true,
            message: '请输入你的用户名哦',
            trigger: 'blur'
          }
        ],
        password: [
          {
            required: true,
            message: '请输入你的密码哦',
            trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    // 提交登录
    handleLoginSubmit () {
      this.$refs.form.validate((valid) => {
        if (valid) {
          //  this.$axios({
          //    url:'/accounts/login',
          //    method:'post',
          //    data:this.form
          //  }).then(res=>{
          //    console.log(res.data);
          //  })
          // 下面这个dispatch的写法应该是dispatch会自动找到store文件夹，然后第一个参数是由文件名和里面的函数构成的
          this.$store.dispatch('user/login', this.form).then((res) => {
            console.log(res)
            this.$message({
              message: `${res.user.username}，欢迎回家`,
              type: 'success'
            })
            setTimeout(() => {
              this.$router.replace('/')
            }, 2000)
          })
        }
      })
    }
  }
}
</script>

<style scoped lang="less">
    .form{
        padding:25px;
    }

    .form-item{
        margin-bottom:20px;
    }

    .form-text{
        font-size:12px;
        color:#409EFF;
        text-align: right;
        line-height: 1;
    }

    .submit{
        width:100%;
        margin-top:10px;
    }
</style>
