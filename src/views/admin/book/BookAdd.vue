<template>
  <div class="page">
    <h4 class="add-title mt-4">Thêm mới sách</h4>
    <BookForm :book="{}" @submit:book="addBook" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import BookForm from '@/components/admin/book/BookForm.vue';
import BookService from "@/services/book.service";

export default {
  components: {
    BookForm,
  },
  data() {
    return {
      message: "",
    };
  },
  methods: {
    async addBook(data) {
      try {
        await BookService.create(data);
        alert("Sách đã được thêm mới thành công");
        this.$router.push({ name: "book" });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

