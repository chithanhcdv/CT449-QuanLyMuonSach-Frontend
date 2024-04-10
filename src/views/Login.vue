<template>
  <div class="row">
    <div class="col-md-3"></div>
    <div class="col">
      <div class="login-form">
        <h2 class="login-title">Đăng nhập</h2>
        <LoginForm @login="handleLogin" />
        <p v-if="error" class="text-danger">{{ error }}</p>
      </div>
    </div>
    <div class="col-md-3"></div>
  </div>
</template>

<script>
import LoginForm from '@/components/admin/LoginForm.vue';
import ReaderService from '@/services/reader.service';

export default {
  components: {
    LoginForm
  },
  data() {
    return {
      error: ''
    };
  },
  methods: {
    async handleLogin(credentials) {
      try {
        const response = await ReaderService.login(credentials);
        const { MADOCGIA } = response.user;

        localStorage.setItem('MADOCGIA', MADOCGIA);
        localStorage.setItem('User_token', true);

        alert("Bạn đã đăng nhập thành công");
        console.log(MADOCGIA);
        this.$router.push({ name: 'homepage' }); 
      } catch (error) {
        this.error = 'Tên đăng nhập hoặc mật khẩu không đúng.';
        console.error(error);
      }
    }
  }
};
</script>

<style>

</style>
