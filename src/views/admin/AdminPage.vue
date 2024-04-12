<script>
import BookService from "@/services/book.service";
import PublisherService from "@/services/publisher.service";
import ReaderService from "@/services/reader.service";
import StaffService from "@/services/staff.service";
import AdminHeader from "@/components/admin/AdminHeader.vue";
import Book from "@/views/admin/book/Book.vue";
import { useRouter } from 'vue-router';
import BorrowBookService from "@/services/borrowBook.service";
import Chart from "chart.js/auto";

export default {
  components: {
    AdminHeader,
    Book,
  },

  data() {
    return {
      bookCount: 0,
      publisherCount: 0,
      readerCount: 0,
      staffCount: 0,
    };
  },

  async created() {
    const isLoggedIn = localStorage.getItem('Admin_token');
    if (!isLoggedIn) {
      const router = useRouter();
      router.push('/admin/login'); 
      return; 
    }

    try {
      const books = await BookService.getAll();
      this.bookCount = books.length;
    } catch (error) {
      console.error("Error fetching books:", error);
    }

    try {
      const publishers = await PublisherService.getAll();
      this.publisherCount = publishers.length;
    } catch (error) {
      console.error("Error fetching publishers:", error);
    }

    try {
      const readers = await ReaderService.getAll();
      this.readerCount = readers.length;
    } catch (error) {
      console.error("Error fetching readers:", error);
    }

    try {
      const staffs = await StaffService.getAll();
      this.staffCount = staffs.length;
    } catch (error) {
      console.error("Error fetching staffs:", error);
    }

    this.renderBorrowBookChart();
  },

  methods: {
  async renderBorrowBookChart() {
    try {
      const borrowBooks = await BorrowBookService.getAll();
      const bookCounts = {};

      borrowBooks.forEach(book => {
        if (bookCounts[book.MASACH]) {
          bookCounts[book.MASACH]++;
        } else {
          bookCounts[book.MASACH] = 1;
        }
      });

      const labels = Object.keys(bookCounts);
      const data = Object.values(bookCounts);

      const ctx = this.$refs.borrowBookChart.getContext("2d");
      new Chart(ctx, {
        type: "bar",
        data: {
          labels: labels,
          datasets: [
            {
              label: "Số lượng sách đã mượn / Mỗi mã độc giả",
              data: data,
              backgroundColor: "rgba(54, 162, 235, 0.2)",
              borderColor: "rgba(54, 162, 235, 1)",
              borderWidth: 1,
            },
          ],
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
            },
          },
        },
      });
    } catch (error) {
      console.error("Error fetching borrowBooks:", error);
    }
  },
},

};
</script>

<template>
  <main>
    <div class="row">
      <div class="col-lg-3 mb-3">
        <div id="book-total" class="total bg-primary">
          <h4>Số lượng sách</h4>
          <div class="flex-total">
            <h4><i class="fa-solid fa-book"></i>{{ bookCount }}</h4>
          </div>
        </div>
      </div>

      <div class="col-lg-3 mb-3">
        <div id="publisher-total" class="total bg-warning">
          <h4>Nhà xuất bản</h4>
          <div class="flex-total">
            <h4><i class="fa-solid fa-home"></i>{{ publisherCount }}</h4>
          </div>
        </div>
      </div>

      <div class="col-lg-3 mb-3">
        <div id="reader-total" class="total bg-success">
          <h4>Độc giả</h4>
          <div class="flex-total">
            <h4><i class="fa-solid fa-users"></i>{{ readerCount }}</h4>
          </div>
        </div>
      </div>

      <div class="col-lg-3 mb-3">
        <div id="staff-total" class="total bg-danger">
          <h4>Nhân viên</h4>
          <div class="flex-total">
            <h4><i class="fa-solid fa-user"></i>{{ staffCount }}</h4>
          </div>
        </div>
      </div>
    </div>
    
    <div class="row">
      <div class="col mb-3">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Biểu số lượng sách được mượn</h5>
            <canvas ref="borrowBookChart" width="400" height="200"></canvas>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
