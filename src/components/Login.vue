<template>
  <div>
    <template>
      <div>
        <Form ref="user" :model="user" :rules="ruleInline" inline>
          <div>
            <FormItem prop="username">
              <Input type="text" v-model="user.userName" placeholder="请输入用户名">
                <Icon type="ios-person-outline" slot="prepend"></Icon>
              </Input>
            </FormItem>
          </div>
          <div>
            <FormItem prop="password">
              <Input type="password" v-model="user.passWd" placeholder="请输入密码">
                <Icon type="ios-lock-outline" slot="prepend"></Icon>
              </Input>
            </FormItem>
          </div>
          <div>
            <FormItem>
              <Button type="primary" @click="login()">登录</Button>
            </FormItem>
          </div>
        </Form>
      </div>
    </template>
  </div>
</template>

<script>
  export default {
    name: 'Login',
    data(){
      return {
        user: {
          userName: '',
          passWd: ''
        },
        ruleInline: {
          userName: [
            { required: true, message: '用户名不能为空', trigger: 'blur' }
          ],
          passWd: [
            { required: true, message: '密码不能为空', trigger: 'blur' },
            { type: 'string', min: 6, message: '密码长度不能小于6', trigger: 'blur' }
          ]
        },
      }
    },
    methods:{
      login(){
        var user = this.user;
        if(user.userName === '' || user.passWd === ''){
          return false;
        }
        this.$axios.post('/api/userController/userLogin',user).then((response) => {
          var status = response.data.code;
          if(status === 200) {
            console.log(response)
            //路由跳转
            this.$router.push('/Helloworld');
          } else {
            alert(response.data);
          }
        }).catch((error) => {
          console.log(response);
        });
      }
    }
  }
</script>
