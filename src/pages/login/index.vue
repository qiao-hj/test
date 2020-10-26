<!-- 登录页 -->
<template>
  <div class="loginPage">
      <form action="" class="formLogin">
          <p>
              用户名<input type="text" placeholder="用户名" v-model="userInfo.username" style="width:100px;height:40px">
          </p>
          <p>
              密&nbsp;&nbsp;&nbsp;码<input type="text" placeholder="密码" v-model="userInfo.password" style="width:100px;height:40px">
          </p>
      </form>
      <button @click="loginHandle" class="loginBtn" type="primary" size="mini">登 录</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
        userInfo: {
            username: "administrator",
            password: "123456789@0",
            validateCode: ""
        }
    };
  },
  methods: {
    loginHandle(){
        // 调用接口
        // let token = wx.getStorageSync('token');
        if(!this.userInfo.username || !this.userInfo.password){
           wx.showToast({
                    title: "用户名或密码不能为空", 
                    icon: 'none',
                    duration: 3000, 
                    mask: true, 
            });
        }else{
            // if(token){
                wx.navigateTo({
                    url:"/pages/logs/main"
                })
            // }else{
            //     wx.showToast({
            //             title: "正在登录", 
            //             icon: 'none',
            //             duration: 3000, 
            //             mask: true, 
            //     });
            //     wx.request({
            //         url: 'http://192.168.5.10:8081/BaseSMVC/admin/system/mobile/login.do',
            //         method:'POST',
            //         header: {
            //             'content-type': 'application/x-www-form-urlencoded; charset=UTF-8'
            //         },
            //         data: this.userInfo,
            //         success (res) {
            //             wx.showToast({
            //                     title: "欢迎回来", 
            //                     icon: 'none',
            //                     duration: 3000, 
            //                     mask: true, 
            //             });
            //              wx.navigateTo({
            //                 url:"/pages/logs/main"
            //             });
            //             wx.setStorageSync('token',res.json);
            //         }
            //     })
            // }
        }
    }
  },
}

</script>
<style lang='scss' scoped>
.loginPage{
    text-align: center;
    padding: 30px;
    box-sizing: border-box;
    button{
        height: 30px;
        line-height: 30px;
        margin-top: 10px;
    }
}
.formLogin{
    p{
        font-size: 12px;
        display: flex;
        align-items: center;
        height: 40px;
        line-height: 40px;
        border-bottom: .5px solid #ccc;
    }
}

</style>