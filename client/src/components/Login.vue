<template>
    <div>
        <h1>User Login</h1>
        <form v-on:submit.prevent="onLogin">
            <p>Email: <input type="email" v-model="email" required /></p>
            <p>Password: <input type="password" v-model="password" required /></p>
            <p><button type="submit">Login</button></p>
        </form>
    </div>
</template>
<script>
import AuthenService from '@/services/AuthenService'
export default {
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async onLogin() {
            try {
                const response = await AuthenService.login({
                    email: this.email,
                    password: this.password
                })
                this.$store.dispatch('setToken', response.data.token)
                this.$store.dispatch('setUser', response.data.user)
                this.$router.push({
                    name: 'users'
                })
            } catch (error) {
                console.log(error)
            }
        }
    }
}

</script>