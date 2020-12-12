<template>
    <div class="login">
        <strong
            v-if="!isFormValid"
            style="color: red;">Giriş Başarız. Bilgilerinizi tekrar kontrol edin</strong>
        <input
            type="text"
            v-model="username"
            placeholder="Kullanıcı Adı" />
        <input
            type="password"
            v-model="password"
            placeholder="Şifre" />
        <button 
            type="button"
            @click="login()">Giriş Yap</button>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Login",
    data() {
        return {
            username: "",
            password: "",
            isFormValid: true
        }
    },
    methods: {
        login() {
            let login = false;
            const self = this;  
            axios.get('https://crudcrud.com/api/8a7c69e399e34f4a8cb229ca7d5a1fe7/users')
            .then(function (response) {
                for (const key in response.data) {
                    if (Object.hasOwnProperty.call(response.data, key)) {
                        const data = response.data[key];
                        if (data.username === self.username && data.password === self.password) {
                            login = true;
                        }
                    }
                }
                if (login) {
                    self.$router.push({ name: 'Home' })
                } else {
                    self.isFormValid = false
                }
            })
            .catch(function (error) {
                console.log(error);
            });
        }
    }
}
</script>

<style lang="scss" scoped>
.login {
    width: 100%;
    max-width: 420px;
    margin: 0 auto;
    padding: 10px;
    background: rgb(230, 230, 230);
    border-radius: 5px;
    input {
        border: 1px solid rgb(214, 214, 214);
        height: 30px;
        width: 100%;
        margin-bottom: 10px;
        padding: 6px;
        border-radius: 5px;
    }
}
</style>