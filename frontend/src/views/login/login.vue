<template>  
    <div>  
        <div class="login-wrap" v-show="showLogin">  
            <h3>登入</h3>  
            <p v-show="showTishi">{{tishi}}</p>  
            <input type="text" placeholder="請輸入用戶名" v-model="username"/>  
            <input type="password" placeholder="請輸入密碼" v-model="password"/>  
            <button v-on:click="login">登入</button>  
            <!--<span v-on:click="ToRegister">没有账号?马上注册</span>-->  
        </div>  
        <!--<div class='register-wrap' v-show="showRegister">  
            <h3>注册</h3>  
            <p v-show="showTishi">{{tishi}}</p>  
            <input type="text" placeholder="请输入用户名" v-model="newUsername"/>  
            <input type="text" placeholder="请输入密码" v-model="newPassword" />  
            <button v-on:click="register">注册</button>  
            <span v-on:click="ToLogin">已有账号?马上登入</span>  
        </div>-->  
    </div>  
</template>  
  
<script>  
    import {setCookie,getCookie} from '../../assets/js/cookie.js'  
    export default{  
        data(){  
            return{  
                username: '',  
                password: '',  
                newUsername: '',  
                newPassword: '',  
                tishi: '',  
                showTishi: false,  
                showLogin: true,  
                showRegister: false  
            }  
        },  
        mounted(){  
            if(getCookie("username")){  
                this.$router.push('/home')  
            }  
        },  
        methods:{  
            login(){  
                if(this.username==""||this.password==""){  
                    alert("請輸入帳號密碼")  
                }else{  
                    // URLSearchParams对象是为了让参数以form data形式  
                    let params = new URLSearchParams();  
                    params.append('username', this.username);  
                    params.append('password', this.password);  
                    this.axios.post("http://52.221.200.234/test",params).then((res)=>{  
                        console.log(res.data)  
                         console.log(typeof res.data)  
                        if(res.data==-1){  
                            this.tishi = "帳號密碼錯誤"  
                            this.showTishi = true  
                        }

                        else if(res.data == 1){  
                             
                       
                            this.tishi = "登入成功"  
                            this.showTishi = true  
                            setCookie("username",this.username,1000*60)
                            setTimeout(function(){  
                                this.$router.push("/home")  
                            }.bind(this),1000)  
                        }  
                    })  
                }  
            }  
        }  
    }  
</script>  
  
<style>  
    .login-wrap{text-align:center;}  
    input{display:block; width:250px; height:40px; line-height:40px; margin:0 auto; margin-bottom: 10px; outline:none; border:1px solid #888; padding:10px; box-sizing:border-box;}  
    p{color:red;}  
    button{display:block; width:250px; height:40px; line-height: 40px; margin:0 auto; border:none; background-color:#41b883; color:#fff; font-size:16px; margin-bottom:5px;}  
    span{cursor:pointer;}  
    span:hover{color:#41b883;}  
</style>    

    <!--      login(){
                console.log('123');
                var params = new URLSearchParams();
                params.append('username',this.username)
                params.append('password',this.password)
                this.axios.post('http://127.0.0.1:5000/test',params        
                )
                .then(function(res){
                  console.log(res.data);
                  if (res.data=='1') {
                    alert('登入成功');
                    setTimeout(function(){  
                                this.$router.push("/home")  
                            }.bind(this),1000)  
                    }
                  else if(res.data == 0){  
                        alert( "請輸入帳號密碼"  )
                        
                    }
                    else if(res.data == 2){  
                        alert("帳號密碼錯誤")  
                        
                    }
                })
                // .catch(function(error) {
                //     alert('留言失敗');
                // })
            } -->