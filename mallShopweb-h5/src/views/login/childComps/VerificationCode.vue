<template>
<el-form-item prop="code">
      <el-input v-model="form.code" autocomplete="off" placeholder="请输入验证码"  style="width:150px;float:left"></el-input>
              <div class="login-code" @click="refreshCode">
                <!--验证码组件-->
                <Verification :identifyCode="identifyCode" />
              </div>
            </el-form-item>
</template>

<script>
import Verification from "../childComps/Verification.vue";
export default {
    name:'VerificationCode',
    components:{
        Verification
    },
data(){  return{
     identifyCodes: "1234567890",
     identifyCode: "",
 }}
 methods:{

//验证码
randomNum(min, max) {
   return Math.floor(Math.random() * (max - min) + min);
},

    refreshCode() {
   this.identifyCode = "";
   this.makeCode(this.identifyCodes, 4);
    },
    makeCode(o, l) {
   for (let i = 0; i < l; i++) {
    this.identifyCode += this.identifyCodes[
    this.randomNum(0, this.identifyCodes.length)
   ];
      }
   console.log(this.identifyCode);
    }

},
created() {
  //初始化验证码
  this.refreshCode();
},
mounted() {
  this.identifyCode = "";
  this.makeCode(this.identifyCodes, 4);
}

</script>

