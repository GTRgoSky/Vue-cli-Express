<template>
  <div class="login-J">
    <input class="form-control" id="inputEmail3" placeholder="请输入账号" v-model="account">
    <input type="password" class="form-control" id="inputPassword3" placeholder="请输入密码" v-model="password">
    <button type="submit" class="btn btn-default" @click="login">登录</button>
    <a href="#/">返回</a>
    <div>{{listdata.get}}</div>
  </div>
</template>

<script>
  export default {
    name: 'flogin',
    data() {
      return {
        account: '',
        password: '',
        listdata:{

        }
      }
    },
    methods: {
      login() {
        // 获取已有账号密码
        var self = this;
        $.ajax({
          url:'/login/getAccount',
          data:{
            "form":"666"
          },
          success(res){
            self.$set(self.listdata,"get",res);
          }
        })
        this.$http.get('/api/login/getAccount')
          .then((response) => {
            // 响应成功回调
            console.log(response)
            let params = {
              account: this.account,
              password: this.password
            };
            // 创建一个账号密码
            return this.$http.post('/api/login/createAccount', params);
          })
          .then((response) => {
            console.log(response)
          })
          .catch((reject) => {
            console.log(reject)
          });
      }
    }
  }

</script>
