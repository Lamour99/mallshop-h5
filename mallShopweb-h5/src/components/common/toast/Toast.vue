<template>
  <div class="toast" v-show="isShow">
      <div>{{message}}</div>
  </div>
</template>

<script>
export default {
    name:'Toast',
    props: {
        message:{
            type:String,
            default:''
        },
        isShow:{
            type:Boolean,
            default:false
        }
    },
    methods: {
        show(message,durtion){
            this.message=message
            this.isShow=true
            setTimeout(() => {
                this.isShow=false
                this.message=''
            }, durtion);
        }
    }
}
</script>

<style>
.toast{
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    padding: 8px 10px;
    color: #ffffff;
    background-color: rgba(0,0,0,0.75);
}
</style>