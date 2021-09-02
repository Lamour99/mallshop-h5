<template>
  <div>
    <public-header></public-header>
    <hr/>
    <Form ref="login" :model="user" :rules="ruleInline" inline>
      <Row>
        <Col span="24">
          <FormItem prop="account">
            <Input type="text" v-model="user.account" placeholder="Account">
              <Icon type="ios-person-outline" slot="prepend"></Icon>
            </Input>
          </FormItem>
        </Col>
      </Row>
      <Row>
        <Col span="24">
          <FormItem prop="password">
            <Input type="password" v-model="user.password" placeholder="Password">
              <Icon type="ios-lock-outline" slot="prepend"></Icon>
            </Input>
          </FormItem>
        </Col>
      </Row>
      <Row>
        <Col span="24">
          <FormItem prop="yzm">
            <Input type="text" v-model="yzm" placeholder="yzm" />
            <div @click="refreshCode">
              <Identify :identifyCode="identifyCode"></Identify>
            </div>
          </FormItem>
        </Col>
      </Row>
      <Row>
        <Col span="24">
          <FormItem>
            <Button type="primary" @click="handleSubmit('login')">登陆</Button>
            <Button type="primary" @click="back">去首页</Button>
          </FormItem>
        </Col>
      </Row>
    </Form>
    <hr/>
    <public-footer></public-footer>
  </div>
</template>
<script>
import Identify from './childComps/Identify.vue'

export default {
  name: 'Login',
  components: {
    Identify
  },
  data () {
    return {
      msg: '这个是登录页',
      identifyCodes: '1234567890',
      identifyCode: '',
      user: {
        account: '',
        password: '',
        verifycode: ''
      },
      ruleInline: {
        account: [{
          required: true,
          message: 'Please fill in the account',
          trigger: 'blur'
        }, {
          type: 'string',
          min: 5,
          message: 'The account length cannot be less than 5 bits',
          trigger: 'blur'
        }],
        password: [{
          required: true,
          message: 'Please fill in the password.',
          trigger: 'blur'
        }, {
          type: 'string',
          min: 6,
          message: 'The password length cannot be less than 6 bits',
          trigger: 'blur'
        }],
        yzm: [{
          required: true,
          message: 'Please fill in the yzm.',
          trigger: 'blur'
        }, {
          type: 'string',
          min: 4,
          message: 'The yzm length cannot be less than 4 bits',
          trigger: 'blur'
        }]
      }
    }
  },
  mounted () {
    this.identifyCode = ''
    this.makeCode(this.identifyCodes, 4)
  },
  methods: {
    handleSubmit (name) {
      this.$refs[name].validate((valid) => {
        if (valid) {
          // 配置默认接口地址，封装参数发送，以下注释中的请求也可以
          /* const para = Object.assign({}, this.user)
            setTimeout(() => {
            login(para).then(res => {
            }).catch(() => {
              // 登陆失败操作
            }, 500)
          }) */
          // 带参发送
          setTimeout(() => {
            login({
              account: this.user.account,
              password: this.user.password
            }).then(res => {
 
            }).catch(() => {
              // 登陆失败操作
            }, 500)
          })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    back () {
      this.$router.push('/')
    },
    // 生成随机数
    randomNum (min, max) {
      return Math.floor(Math.random() * (max - min) + min)
    },
    // 切换验证码
    refreshCode () {
      this.identifyCode = ''
      this.makeCode(this.identifyCodes, 4)
    },
    // 生成四位随机验证码
    makeCode (o, l) {
      for (let i = 0; i < l; i++) {
        this.identifyCode += this.identifyCodes[
          this.randomNum(0, this.identifyCodes.length)
          ]
      }
      console.log(this.identifyCode)
    }
  }
}
</script>
<style lang="postcss" scoped>
    body {
        background-color: #ff0000;
    }
</style>