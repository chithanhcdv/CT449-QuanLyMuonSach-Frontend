<template>
  <div class="row">
    <div class="col-md-3"></div>
    <div class="col">
      <div class="login-form">
        <h2 class="login-title">Đăng nhập nhân viên</h2>
        <LoginForm @login="handleLogin" />
        <p v-if="error" class="text-danger">{{ error }}</p>
      </div>
    </div>
    <div class="col-md-3"></div>
  </div>
</template>

<script>
import LoginForm from '@/components/admin/LoginForm.vue';
import StaffService from '@/services/staff.service';

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
        await StaffService.login(credentials);
        localStorage.setItem('Admin_token', true);
        this.isLoggedIn = true;
        alert("Bạn đã đăng nhập thành công");
        this.$router.push({ name: 'adminPage' }); 
      } catch (error) {
        this.error = 'Tên đăng nhập hoặc mật khẩu không đúng.';
        console.error(error);
      }
    }
  }
};
</script>

