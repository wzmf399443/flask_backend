<template>  
    <div>  
        <h3>歡迎{{name}}</h3>  
        <!-- 教程中href是#，但是我测试注销后不能自动跳到 -->  
        <a href="/" v-on:click="quit">登出</a>  
    </div>  
</template>  
  
<script>  
import {setCookie,getCookie,delCookie} from '../../assets/js/cookie.js'  
export default{  
    data(){  
        return{  
            name:""  
        }  
    },  
    mounted(){  
        let uname = getCookie("username")  
        this.name = uname  
        if(uname == ""){  
            this.$router.push("/")  
        }  
    },  
    methods:{  
        quit(){  
            delCookie("username")  
        }  
    }  
}  
</script>  
  
<style>  
</style>  