<template>
  <div>
    <h2>Đăng ký tài khoản</h2>
    <RegisterForm @register="handleRegister" />
  </div>
</template>

<script>
import RegisterForm from "@/components/RegisterForm.vue";
import ReaderService from "@/services/reader.service";

export default {
  components: {
    RegisterForm,
  },
  methods: {
    async handleRegister(data) {
      try {
        await ReaderService.register(data);
        alert("Đăng ký thành công");
        this.$router.push({ name: "homepage" });
      } catch (error) {
        console.log(error);
        alert("Đăng ký thất bại");
      }
    },
  },
};
</script>

<style scoped>
/* Các quy tắc CSS cụ thể cho trang Register.vue */
</style>
