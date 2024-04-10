<template>
  <header>
    <div class="container">
      <div class="row">
        <div class="col-md-2 icon-div">
          <router-link to="/">
            <img src="C:\CT449-BTL\QuanLyMuonSach-Frontend\src\assets\images\icon.png" class="img-fluid icon">
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
                    <a class="nav-link fw-bold fs-5" href="#">TRANG CHỦ</a>
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
          <div class="d-flex align-items-center">       
            <div v-if="isLoggedIn" class="dropdown" id="dropdown-user">
              <button class="btn btn " type="button" data-bs-toggle="dropdown">
                <i class="fa-solid fa-user fa-3x header-icon" id="user-icon"></i>
              </button>
              <ul class="dropdown-menu">
                <li><button @click="logout" class="nav-link">Đăng xuất</button></li>
              </ul>    
            </div>
            <div v-else class="dropdown" id="dropdown-user">
              <button class="btn btn " type="button" data-bs-toggle="dropdown">
                <i class="fa-solid fa-user fa-2x header-icon" id="user-icon"></i>
              </button>
              <ul class="dropdown-menu">
                <li><router-link to="/login" class="nav-link">Đăng nhập</router-link></li>
                <li><router-link to="/register" class="nav-link">Đăng ký</router-link></li>
              </ul>    
            </div>
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
      // Xử lý đăng xuất ở đây
      localStorage.removeItem('User_token');
      localStorage.removeItem('MADOCGIA');
      this.isLoggedIn = false;
      alert("Bạn đã đăng xuất thành công");
      this.$router.push({ name: 'homepage' });
    },

    checkLoginStatus() {
      const token = localStorage.getItem("User_token");
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
.icon{
  border: 0cap;
  width: 45%;
}

.icon-div{
  text-align: center;
}

header{
  background-color: white;
}

.search-input{
  margin-top: 25px;
  width: 70%;
  height:50%;
  margin-right: 20%;
}

.header-menu{
  display: flex;
  justify-content:space-between;
}

.nav-item{
  padding-right: 50px;
}

.nav-link:hover{
  color: greenyellow;
  font-weight: bold;
}

</style>
