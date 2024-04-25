<template>
  <header id="header-user">
    <div class="container">
      <div class="row">
        <div class="col-md-2 icon-div">
          <router-link :to="{ name:'homepage' }">
            <img src="@/assets/images/icon.png" class="img-fluid icon">
          </router-link>
        </div>                 
        <div class="col-md-10 header-menu">
          <nav class="navbar navbar-expand-lg">
            <div class="container-fluid">
              <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
              </button>
              <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                  <li class="nav-item">
                    <router-link :to="{ name:'homepage'}" class="nav-link fw-bold fs-5">TRANG CHỦ</router-link>
                  </li>
                  <li class="nav-item">
                    <a class="nav-link fw-bold fs-5" href="#">VỀ THƯ VIỆN</a>
                  </li>
                  <li class="nav-item">
                    <a class="nav-link fw-bold fs-5" href ="#">NỘI QUY THƯ VIỆN</a>
                  </li>
                   <li class="nav-item">
                    <a class="nav-link fw-bold fs-5" href ="#">LIÊN HỆ</a>
                  </li>
                </ul>
              </div>
            </div>
          </nav>        
          <div v-if="isLoggedIn" class="d-flex align-items-center dropup-center dropup">       
            <button class="btn btn border-0" type="button" data-bs-toggle="dropdown" aria-expanded="false">
              <i class="fa-solid fa-user fa-2x header-icon" id="user-icon"></i>
            </button>
            <ul class="dropdown-menu text-center">
              <li><router-link :to="{ name:'reader.information'}" class="nav-link dropdown-item fw-bold fs-5 mb-2">Thông tin độc giả</router-link></li>
              <li><router-link :to="{ name:'borrowBook.history'}" class="nav-link dropdown-item fw-bold fs-5 mb-2">Thông tin mượn sách</router-link></li>
              <li><button @click="logout" class="nav-link dropdown-item fw-bold fs-5 mb-2">Đăng xuất</button></li>
            </ul>   
          </div> 
          <div v-else class="d-flex align-items-center dropup-center dropup">     
            <button class="btn btn border-0" type="button" data-bs-toggle="dropdown">
              <i class="fa-solid fa-user fa-2x header-icon" id="user-icon"></i>
            </button>
            <ul class="dropdown-menu text-center">
              <li><router-link :to="{ name:'reader.login'}" class="nav-link dropdown-item fw-bold fs-5 mb-2">Đăng nhập</router-link></li>
              <li><router-link :to="{ name:'reader.register'}" class="nav-link dropdown-item fw-bold fs-5 mb-2">Đăng ký</router-link></li>
            </ul>    
          </div>  
        </div> 
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      isLoggedIn: false
    };
  },
  methods: {
    logout() {
      localStorage.removeItem('User_token');
      localStorage.removeItem('MADOCGIA');
      this.isLoggedIn = false;
      this.showAlert("Bạn đã đăng xuất thành công", "success")
      this.$router.push({ name: 'homepage' });
    },

    checkLoginStatus() {
      const token = localStorage.getItem("User_token");
      this.isLoggedIn = !!token;
    },

    showAlert(message, type) {
      const icon = {
        success: "✅",
        error: "❌"
      }[type];

      alert(`${icon} ${message}`);
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