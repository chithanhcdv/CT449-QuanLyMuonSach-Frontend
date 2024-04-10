<script>
import BookService from "@/services/book.service";
import AdminHeader from "@/components/admin/AdminHeader.vue";
import Book from "@/views/admin/book/Book.vue";
import { useRouter } from 'vue-router';

export default {
  components: {
    AdminHeader,
    Book
  },

  data() {
    return {
      bookCount: 0
    };
  },

  async created() {
    const isLoggedIn = localStorage.getItem('Admin_token');
    if (!isLoggedIn) {
      const router = useRouter();
      router.push('/admin/login'); 
      return; 
    }

    // Gọi phương thức để lấy số lượng sách từ dịch vụ
    try {
      const books = await BookService.getAll();
      this.bookCount = books.length;
    } catch (error) {
      console.error("Error fetching books:", error);
    }
  }
};
</script>


<template>
  <main>
    <div class="row">
      <div class="col-lg-3 mb-3">
          <div id="book-total" class="total bg-primary">
              <h4>Số lượng sách</h4>
              <div class="flex-total">  
                <h4> <i class="fa-solid fa-book"></i>{{ bookCount }}</h4>
              </div>
          </div>
      </div>

      <div class="col-lg-3 mb-3">
          <div id="publisher-total" class="total bg-warning">
              <h4>Nhà xuất bản</h4>
              <div class="flex-total">
                  <p><i class="fa-solid fa-home"></i></p>
              </div>
          </div>
      </div>

      <div class="col-lg-3 mb-3">
          <div id="reader-total" class="total bg-success">
              <h4>Độc giả</h4>
              <div class="flex-total">
                  <p><i class="fa-solid fa-users"></i></p>
              </div>
          </div>
      </div>

      <div class="col-lg-3 mb-3">
          <div id="staff-total" class="total bg-danger">
              <h4>Nhân viên</h4>
              <div class="flex-total">
                  <p><i class="fa-solid fa-user"></i></p>
              </div>
          </div>
      </div>
    </div>
  </main>

</template>

