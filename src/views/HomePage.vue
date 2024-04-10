<template>
  <main>
    <div class="banner">
      <img src="C:\CT449-BTL\QuanLyMuonSach-Frontend\src\assets\images\banner.png" alt="">
    </div>
    <div class="container">
      <div class="input-group mt-5 search-input">
        <input type="text" v-model="searchKeyword" class="form-control" placeholder="Nhập tên sách" aria-label="Recipient's username" aria-describedby="basic-addon2" id="searchInput" name="name" @keydown.enter="search">
        <button @click="search" class="input-group-text" type="submit"><span class="" id="basic-addon2"><i class="fa-solid fa-magnifying-glass"></i></span></button>
        <button @click="resetSearch" class="input-group-text" type="button"><span class="" id="basic-addon2"><i class="fa-solid fa-redo"></i></span></button>
      </div>
      <div id="main-page">
        <div class="row">
          <div class="col-md-3" v-for="book in books" :key="book._id">
            <router-link :to="{ name: 'book.detail', params: { id: book._id } }">
              <div class="card mb-4 bg-white">
                <img :src="book.HINHANH" class="card-img-top" alt="Book Image">
                <div class="card-body">
                  <h5 class="card-title text-truncate">{{ book.TENSACH }}</h5>
                  <h5 class="card-title text-truncate">{{ book.MASACH }}</h5>
                  <div class="borrow-button">
                    <button class="btn btn-primary" @click="openModal(book)">Mượn</button>
                  </div>
                </div>
              </div>
            </router-link>
          </div>
        </div>
      </div>

      <div class="modal" :class="{ 'show': showModal }">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Mượn sách: {{ selectedBook.TENSACH }}</h5>
              <button type="button" class="btn-close" aria-label="Close" @click="closeModal"></button>
            </div>
            <div class="modal-body">
              <div class="mb-3">
                <label for="note" class="form-label">Ghi chú:</label>
                <textarea class="form-control" id="note" v-model="note"></textarea>
              </div>
              <div class="mb-3">
                <label for="borrowDate" class="form-label">Ngày mượn:</label>
                <input type="date" class="form-control" id="borrowDate" v-model="borrowDate">
              </div>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" @click="closeModal">Đóng</button>
              <button type="button" class="btn btn-primary" @click="borrowBook">Mượn sách</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import BookService from "@/services/book.service";
import BorrowBookService from "@/services/borrowBook.service";
import AdminHeader from "@/components/admin/AdminHeader.vue";

export default {
  components: {
    AdminHeader,
  },

  data() {
    return {
      books: [],
      showModal: false,
      selectedBook: '',
      note: '',
      borrowDate: '',
      searchKeyword: ''
    };
  },

  async created() {
    try {
      await this.fetchBooks();
    } catch (error) {
      console.error("Error fetching books:", error);
    }
  },

  methods: {
    async fetchBooks() {
      try {
        this.books = await BookService.getByName(this.searchKeyword);
      } catch (error) {
        console.error("Error fetching books:", error);
      }
    },

    openModal(book) {
      this.showModal = true;
      this.selectedBook = book;
    },

    // Function to close modal
    closeModal() {
      this.showModal = false;
      this.selectedBook = '';
      this.note = '';
      this.borrowDate = '';
    },
    
    async borrowBook() {
      try {
        const response = await BorrowBookService.create({
          MADOCGIA: localStorage.getItem('MADOCGIA'),
          MASACH: this.selectedBook.MASACH,
          GHICHU: this.note,
          NGAYMUON: this.borrowDate
        });
        console.log("Borrow Book Response:", response);
        alert("Mượn sách thành công");
        this.closeModal();
      } catch (error) {
        console.error("Error borrowing book:", error);
      }
    },

    async search() {
      try {
        await this.fetchBooks(); 
      } catch (error) {
        console.error("Error searching books:", error);
      }
    },
    
    resetSearch() {
      this.searchKeyword = '';
      this.fetchBooks();
    }
  }
};
</script>


<style scoped>
.borrow-button{
  text-align: center;
}

.search-input{
  width: 50%;
  margin: 0 auto;
}
</style>
