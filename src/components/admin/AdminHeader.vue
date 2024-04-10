<template>
  <header class="mt-3">
    <nav class="navbar navbar-dark bg-dark">
      <div class="container">
        <router-link to="/admin" class="navbar-brand">Admin Panel</router-link>
        <button class="navbar-toggler me-auto" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasWithBackdrop" aria-controls="offcanvasWithBackdrop">
          <span class="navbar-toggler-icon"></span>
        </button>
      </div>
    </nav>  
    
    <!-- Offcanvas container -->
    <div class="offcanvas offcanvas-start text-bg-dark" tabindex="-1" id="offcanvasWithBackdrop" aria-labelledby="offcanvasWithBackdropLabel">
      <div class="offcanvas-header">
        <h5 class="offcanvas-title" id="offcanvasWithBackdropLabel">Offcanvas</h5>
        <button type="button" class="btn-close btn-close-white text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
      </div>
      <div class="offcanvas-body">
        <!-- Offcanvas content -->
        <ul class="navbar-nav">
            <li class="nav-item" :class="{ 'active': $route.path === '/admin' }">
                <router-link to="/admin" class="nav-link"><i class="fa-solid fa-home"></i>Home</router-link>
            </li>  
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/book' }">
                <router-link to="/admin/book" class="nav-link"><i class="fa-solid fa-book"></i>Quản lý sách</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/publisher' }">
                <router-link to="/admin/publisher" class="nav-link"><i class="fa-solid fa-shop"></i>Nhà xuất bản</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/reader' }">
                <router-link to="/admin/reader" class="nav-link"><i class="fa-solid fa-users"></i>Độc giả</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/staff' }">
                <router-link to="/admin/staff" class="nav-link"><i class="fa-solid fa-user"></i>Nhân viên</router-link>
            </li>
            <li class="nav-item" :class="{ 'active': $route.path === '/admin/borrowBook' }">
                <router-link to="/admin/borrowBook" class="nav-link"><i class="fa-solid fa-check"></i>Muợn trả</router-link>
            </li>
            <hr>

            <!-- Kiểm tra nếu đã đăng nhập -->
            <template v-if="isLoggedIn">
                <li class="nav-item" @click="logout">
                    <a href="#" class="nav-link"><i class="fa-solid fa-sign-out"></i>Đăng xuất</a>
                </li>
            </template>
            <!-- Nếu chưa đăng nhập, hiển thị liên kết đăng nhập -->
            <template v-else>
                <li class="nav-item" :class="{ 'active': $route.path === '/admin/login' }">
                    <router-link to="/admin/login" class="nav-link"><i class="fa-solid fa-right-to-bracket"></i>Đăng nhập</router-link>
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
      this.$router.push("/admin/login");
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
nav{
    padding:10px;
    padding-left:20px
}

header .offcanvas-start {
  width: 250px; 
}

li{
    margin-bottom: 20px;
}

li:hover{
  color: red;
  font-weight: bold;
}

.active {
    color: red; 
    font-weight: bold; 
}
</style>
