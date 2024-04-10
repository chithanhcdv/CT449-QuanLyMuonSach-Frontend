<template>
  <form @submit.prevent="login">
    <div class="form-group">
      <input type="text" class="form-control" id="username" v-model="username" maxlength="20" placeholder="Tên tài khoản" required>
    </div>
    <div class="form-group">
      <input type="password" class="form-control" id="password" v-model="password" minlength="6" placeholder="Mật khẩu" required>
    </div>
    <div class="login-button">
      <button type="submit" class="btn btn-primary">Đăng nhập</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: ''
    };
  },
  methods: {
    login() {
      // Đưa thông tin đăng nhập vào hàm login để xử lý
      this.$emit('login', {
        USERNAME: this.username,
        PASSWORD: this.password
      });
    }
  }
};
</script>
