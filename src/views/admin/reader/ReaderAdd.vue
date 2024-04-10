<template>
  <div class="page">
    <h4 class="add-title mt-4">Thêm mới độc giả</h4>
    <ReaderForm :reader="{}" @submit:reader="addReader" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ReaderForm from '@/components/admin/reader/ReaderForm.vue';
import ReaderService from "@/services/reader.service";

export default {
  components: {
    ReaderForm,
  },
  data() {
    return {
      message: "",
    };
  },
  methods: {
    async addReader(data) {
      try {
        await ReaderService.register(data);
        alert("Độc giả đã được thêm mới thành công");
        this.$router.push({ name: "reader" });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
