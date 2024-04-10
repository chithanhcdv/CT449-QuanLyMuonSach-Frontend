<template>
  <Form
    @submit="submitBook"
    :validation-schema="bookFormSchema"
  >
    <!-- Các trường nhập sách -->

    <div class="form-group">
      <label for="readerId">Mã độc giả</label>
      <Field
        name="readerId"
        type="text"
        class="form-control"
        v-model="bookLocal.MADOCGIA"
      />
      <ErrorMessage name="readerId" class="error-feedback" />
    </div>

    <div class="form-group">
      <label for="bookId">Mã sách</label>
      <Field
        name="bookId"
        type="text"
        class="form-control"
        v-model="bookLocal.MASACH"
      />
      <ErrorMessage name="bookId" class="error-feedback" />
    </div>

    <div class="form-group">
      <label for="note">Ghi chú</label>
      <Field
        name="note"
        type="text"
        class="form-control"
        v-model="bookLocal.GHICHU"
      />
      <ErrorMessage name="note" class="error-feedback" />
    </div>

    <div class="form-group">
      <label for="borrowDate">Ngày mượn</label>
      <Field
        name="borrowDate"
        type="date"
        class="form-control"
        v-model="bookLocal.NGAYMUON"
      />
      <ErrorMessage name="borrowDate" class="error-feedback" />
    </div>

    <div class="form-group">
      <label for="returnDate">Ngày trả</label>
      <Field
        name="returnDate"
        type="date"
        class="form-control"
        v-model="bookLocal.NGAYTRA"
      />
      <ErrorMessage name="returnDate" class="error-feedback" />
    </div>

    <!-- Nút thêm hoặc cập nhật sách -->
  </Form>
</template>

<script>
import * as yup from 'yup';
import { Form, Field, ErrorMessage } from "vee-validate";

export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  emits: ["submit:book", "delete:book"],
  props: {
    book: { type: Object, required: true }
  },
  data() {
    const bookFormSchema = yup.object().shape({
      // Các quy tắc xác thực cho mượn sách
      readerId: yup
        .string()
        .required("Mã độc giả không được để trống"),
      bookId: yup
        .string()
        .required("Mã sách không được để trống"),
      note: yup.string(),
      borrowDate: yup.date().required("Ngày mượn không được để trống"),
      returnDate: yup.date().required("Ngày trả không được để trống"),
    });
    return {
      bookLocal: { ...this.book },
      bookFormSchema,
    };
  },
  computed: {
    isEditMode() {
      return !!this.bookLocal._id;
    }
  },
  methods: {
    submitBook() {
      this.$emit("submit:book", this.bookLocal);
    },
    deleteBook() {
      this.$emit("delete:book", this.bookLocal._id);
    },
  },
};
</script>

<style scoped>
/* CSS tùy chỉnh cho BorrowBookForm */
</style>
