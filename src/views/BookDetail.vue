<template>
  <div class="container">
    <div class="card mt-5 mb-5 bg-white">
        <div class="row">
            <div class="col image-detail"><img :src="book.HINHANH" class="card-img-top" alt="Book Image"></div>
            <div class="col">
                <div class="card-body">
                    <p class="card-title fw-bold fs-4 ">{{ book.TENSACH }}</p>
                    <p class="card-text">Tác giả: {{ book.TACGIA }}</p>
                    <p class="card-text">Số quyển: {{ book.SOQUYEN }}</p>
                    <p class="card-text">Đơn giá: {{ book.DONGIA }}đ</p>
                    <p class="card-text">Tên Nhà xuất bản: {{ publisher.TENNXB }}</p>
                    <p class="card-text">Năm xuất bản: {{ book.NAMXUATBAN }}</p>
                    <p class="card-text">Thể loại: {{ book.THELOAI }}</p>
                    <p class="card-text">Mô tả: {{ book.MOTA }}</p>
                    <div class="borrow-button mt-3">
                        <button class="btn btn-primary" @click="openModal">Mượn</button>
                    </div>
                </div>
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
</template>

<script>
import BookService from "@/services/book.service";
import BorrowBookService from "@/services/borrowBook.service";
import PublisherService from "@/services/publisher.service"; // Import PublisherService

export default {
  data() {
    return {
      book: {},
      showModal: false,
      selectedBook: '',
      note: '',
      borrowDate: '',
      publisher: null 
    };
  },
  async created() {
    try {
      const bookId = this.$route.params.id;
      this.book = await BookService.getById(bookId);

      const publishers = await PublisherService.getAll();

      this.publisher = publishers.find(pub => pub.MANXB === this.book.MANXB);
    } catch (error) {
      console.error("Error fetching book detail:", error);
    }
  },
  methods: {
    openModal() {
      this.showModal = true;
      this.selectedBook = this.book;
    },
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
    }
  }
};
</script>
