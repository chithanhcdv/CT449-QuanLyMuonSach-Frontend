<template>
  <div class="page">
    <h4 class="add-title mt-4">Thêm mới nhân viên</h4>
    <StaffForm :staff="{}" @submit:staff="addStaff" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import StaffForm from '@/components/admin/staff/StaffForm.vue';
import StaffService from "@/services/staff.service";

export default {
  components: {
    StaffForm,
  },
  data() {
    return {
      message: "",
    };
  },
  methods: {
    async addStaff(data) {
      try {
        await StaffService.create(data);
        alert("Nhân viên đã được thêm mới thành công");
        this.$router.push({ name: "staff" });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
