<template>
<div>
    <h1>แก้ไขข้อมูล</h1>
    <form v-on:submit.prevent = "editUser">
        <p>name: <input type="text" v-model="user.name"></p>
        <p>lastname: <input type="text" v-model="user.lastname"></p>
        <p>Bag Style: <input type="text" v-model="user.password"></p>
        <p>ราคากระเป๋า: <input type="text" v-model="user.email"></p>
        <p><button type="submit">ยื่นยันข้อมูล</button></p>
    </form>
    <hr>
    <div>
        <p>name: {{user.name}}</p>
        <p>lastname: {{user.lastname}}</p>
        <p>Bag Style: {{ user.password }}</p>
        <p>ราคากระเป๋า: {{ user.email }}</p>
    </div>
</div>
</template>
<script>import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async editUser(){
            try{
                await UsersService.put(this.user)
                this.$router.push({
                    name: 'users'
                })

            }catch(error){
                console.log(error)
            }
        }
    }, 
    async created(){
        try{
            let userId = this.$route.params.userId
            this.user = (await UsersService.show(userId)).data
        }catch(error){
            console.log(error)
        }
    }
}
</script>
<style scoped>


</style>