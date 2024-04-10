<template>
  <div id="app" :class="{ 'non-admin-background': !isAdminRoute }">
    <AppHeader v-if="!isAdminRoute"/> <!-- Use AppHeader for non-admin routes -->
    <AdminHeader v-if="isAdminRoute"/> <!-- Use AdminHeader for admin routes -->
    <div class="" v-if="!isAdminRoute">
      <router-view />
    </div>
    <div class="container mt-3" v-if="isAdminRoute">
      <router-view />
    </div>
    <AppFooter v-if="!isAdminRoute"/>
  </div>
</template>

<script>
import AppHeader from "@/components/AppHeader.vue";
import AppFooter from "@/components/AppFooter.vue";
import AdminHeader from "@/components/admin/AdminHeader.vue";

export default {
  components: {
    AppHeader,
    AppFooter,
    AdminHeader,
  },
  computed: {
    isAdminRoute() {
      return this.$route.path.startsWith("/admin");
    },
  },
};
</script>

<style>
.non-admin-background {
  background-color: whitesmoke;
}
</style>
