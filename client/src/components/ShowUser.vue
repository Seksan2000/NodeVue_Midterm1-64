<template>
  <div>
    <h1>ข้อมูลผู้ซื้อ</h1>
    <p> {{ userId }}</p>
    <p>ชื่อ - นามสกุล {{ user.name }} - {{ user.lastname }}</p>
    <p>Bag Style: {{ user.password }}</p>
    <p>ราคากระเป๋า: {{ user.email }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>