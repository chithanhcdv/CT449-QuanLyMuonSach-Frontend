<template>
  <header id="header-admin">
    <nav class="navbar navbar-dark bg-dark p-3">
      <div class="container">
        <router-link :to="{ name:'adminPage' }" class="navbar-brand fw-bold fs-3">HOME</router-link>
        <button class="navbar-toggler me-auto" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasWithBackdrop" aria-controls="offcanvasWithBackdrop">
          <span class="navbar-toggler-icon"></span>
        </button>
      </div>
    </nav>  
    
    <div class="offcanvas offcanvas-start text-bg-dark" tabindex="-1" id="offcanvasWithBackdrop" aria-labelledby="offcanvasWithBackdropLabel">
      <div class="offcanvas-header">
        <h5 class="offcanvas-title fw-bold" id="offcanvasWithBackdropLabel">Admin Panel</h5>
        <button type="button" class="btn-close btn-close-white text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
      </div>
      <div class="offcanvas-body">
        <ul class="navbar-nav">
            <li class="nav-item" :class="{ 'active': $route.path === '/admin' }">
              <router-link :to="{ name:'adminPage' }" class="nav-link fw-bold"><i class="fa-solid fa-home"></i>Home</router-link>
            </li>  
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/book' }">
              <router-link :to="{ name:'book' }" class="nav-link fw-bold"><i class="fa-solid fa-book"></i>Quản lý sách</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/publisher' }">
              <router-link :to="{ name:'publisher' }" class="nav-link fw-bold"><i class="fa-solid fa-shop"></i>Nhà xuất bản</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/reader' }">
              <router-link :to="{ name:'reader' }" class="nav-link fw-bold"><i class="fa-solid fa-users"></i>Độc giả</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/staff' }">
              <router-link :to="{ name:'staff' }" class="nav-link fw-bold"><i class="fa-solid fa-user"></i>Nhân viên</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/borrowBook' }">
              <router-link :to="{ name:'borrowBook' }" class="nav-link fw-bold"><i class="fa-solid fa-check"></i>Muợn trả</router-link>
            </li>
            <hr>

            <li class="nav-item">
              <a href="#" class="nav-link fw-bold"><i class="fa-solid fa-bell"></i>Thông báo</a>
            </li>

            <li class="nav-item">
              <a href="#" class="nav-link fw-bold"><i class="fa-solid fa-envelope"></i>Hộp thư</a>
            </li>
           
            <template v-if="isLoggedIn">
                <li class="nav-item" @click="logout">
                    <a href="#" class="nav-link fw-bold"><i class="fa-solid fa-sign-out"></i>Đăng xuất</a>
                </li>
            </template>
          
            <template v-else>
                <li class="nav-item" :class="{ 'active': $route.path === '/admin/login' }">
                    <router-link :to="{ name:'staff.login' }" class="nav-link fw-bold"><i class="fa-solid fa-right-to-bracket"></i>Đăng nhập</router-link>
                </li>
            </template>
        </ul>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "AdminHeader",
  data() {
    return {
      isLoggedIn: false
    };
  },
  methods: {
    logout() {
      localStorage.removeItem("Admin_token");
      this.isLoggedIn = false;
      alert("Bạn đã đăng xuất thành công");
      this.$router.push({ name:'staff.login' });
    },

    checkLoginStatus() {
      const token = localStorage.getItem("Admin_token");
      this.isLoggedIn = !!token;
    }
  },

  mounted() {
    this.checkLoginStatus();
  },

  watch: {
    '$route'() {
      this.checkLoginStatus();
    }
  }
};
</script>

<style scoped>
header .offcanvas-start {
  width: 250px; 
}
</style>
