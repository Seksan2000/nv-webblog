<template>
<div>
    <h1>Edit User</h1>
    <form v-on:submit.prevent = "editUser">
        <p>Name : <input type="text" v-model="user.name"></p>
        <p>Lastname : <input type="text" v-model="user.lastname"></p>
        <p>Email : <input type="text" v-model="user.email"></p>
        <p>Password : <input type="text" v-model="user.password"></p>
        <p><button type="submit">Edit User</button></p>
    </form>
    <hr>
    <div>
        <p>Name : {{user.name}}</p>
        <p>Lastname : {{user.lastname}}</p>
        <p>Email : {{user.email}}</p>
        <p>Password : {{user.password}}</p>
    </div>
</div>
</template>
<script>
import UserService from '@/services/UserService'
export default {
    data() {
        return {
            user: {
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods: {
        async editUser() {
            try {
                await UserService.put(this.user)
                this.$router.push({
                    name: 'user'
                })
            } catch (error) {
                console.log(error)
            }
        }
    },
    async created() {
        try {
           let userId = this.$route.params.userId
           this.user = (await UserService.show(userId)).data 
        } catch (error) {
            console.log (error)
        }
    }
}
</script>
<style scoped>
</style>