<template>
  <form @submit.prevent="register">
    <div class="form-group">
      <label for="username">Username</label>
      <input type="text" id="username" v-model="username" class="form-control" required>
    </div>
    <div class="form-group">
      <label for="password">Password</label>
      <input type="password" id="password" v-model="password" class="form-control" required>
    </div>
    <div class="form-group">
      <label for="hoLot">Họ lót</label>
      <input type="text" id="hoLot" v-model="hoLot" class="form-control" required>
    </div>
    <div class="form-group">
      <label for="ten">Tên</label>
      <input type="text" id="ten" v-model="ten" class="form-control" required>
    </div>
    <div class="form-group">
      <label for="ngaySinh">Ngày sinh</label>
      <input type="date" id="ngaySinh" v-model="ngaySinh" class="form-control" required>
    </div>
    <div class="form-group">
      <label for="phai">Giới tính</label>
      <select id="phai" v-model="phai" class="form-control" required>
        <option value="Nam">Nam</option>
        <option value="Nữ">Nữ</option>
      </select>
    </div>
    <div class="form-group">
      <label for="diaChi">Địa chỉ</label>
      <input type="text" id="diaChi" v-model="diaChi" class="form-control" required>
    </div>
    <div class="form-group">
      <label for="dienThoai">Điện thoại</label>
      <input type="text" id="dienThoai" v-model="dienThoai" class="form-control" required>
    </div>
    <button type="submit" class="btn btn-primary">Register</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      hoLot: '',
      ten: '',
      ngaySinh: '',
      phai: '',
      diaChi: '',
      dienThoai: ''
    };
  },
  methods: {
    register() {
      // Đưa thông tin đăng ký vào sự kiện emit để xử lý ở thành phần cha
      this.$emit('register', {
        USERNAME: this.username,
        PASSWORD: this.password,
        HOLOT: this.hoLot,
        TEN: this.ten,
        NGAYSINH: this.ngaySinh,
        PHAI: this.phai,
        DIACHI: this.diaChi,
        DIENTHOAI: this.dienThoai
      });
    }
  }
};
</script>

<style scoped>
/* Add your component-specific styles here */
</style>
