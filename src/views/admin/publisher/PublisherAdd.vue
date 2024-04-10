<template>
  <div class="page">
    <h4 class="add-title mt-4">Thêm mới nhà xuất bản</h4>
    <PublisherForm :publisher="{}" @submit:publisher="addPublisher" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import PublisherForm from '@/components/admin/publisher/PublisherForm.vue';
import PublisherService from "@/services/publisher.service";

export default {
  components: {
    PublisherForm,
  },
  data() {
    return {
      message: "",
    };
  },
  methods: {
    async addPublisher(data) {
      try {
        await PublisherService.create(data);
        alert("Nhà xuất bản đã được thêm mới thành công");
        this.$router.push({ name: "publisher" });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
