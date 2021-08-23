<template>
  <div>
    <h1>All User Bag Order List</h1>
    <div v-if="users.length">
      <h4>จำนวนลูกค้าที่สั่ง {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            เพิ่มออเดอร์สิน
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
        <p>id: {{ user.id }}</p>
        <p>ชื่อ-นามสกุล: {{ user.name }} - {{ user.lastname }}</p>
        <p>Bag Style: {{ user.password }}</p>
        <p>ราคากระเป๋า: {{ user.email }}</p>
        <p>
          <button v-on:click="navigateTo('/user/' + user.id)">
           ดูข้อมูลลูกค้า
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            แก้ไขข้อมูล
          </button>
          <button v-on:click="deleteUser(user)">
            ลบข้อมูล
          </button>
        </p>
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: [],
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user){
      let result = confirm("Want to delete")
      if(result){
        try{
          await UsersService.delete(user)
          this.refreshData()
        }catch(error){
          console.log(error)
        }
      }
    },
    async refreshData(){
      this.users = (await UsersService.index()).data
    }
  },
};
</script>
<style scoped>
</style>