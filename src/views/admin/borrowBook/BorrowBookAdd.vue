<template>
  <div>
    <h2>Add Borrow Book</h2>
    <BorrowBookForm @submit="addBorrowBook" />
  </div>
</template>

<script>
import BorrowBookForm from "@/components/admin/borrowBook/BorrowBookForm.vue";
import BorrowBookService from "@/services/borrowBook.service";

export default {
  components: {
    BorrowBookForm
  },
  methods: {
    async addBorrowBook(data) {
      try {
        await BorrowBookService.create(data);
        alert("Borrow Book added successfully");
        this.$router.push("/borrow-books");
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>
