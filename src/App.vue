<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <HelloWorld msg="Welcome to Your Vue.js App"/>
    </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

export default {
    name: 'app',
    components: {
        HelloWorld
    },
    created() {
        const postData = {
            grant_type: 'password',
            client_id: 2,
            client_secret: 'H46RgGdh9OPQALRJm48UPjnlIuhsbL0bfWlViJFU',
            username: 'alex@example.com',
            password: 'secret',
            scope: '',
        }

        axios.post('http://laravel-api-server.test/oauth/token', postData)
            .then(response => {
                const accessToken = response.data.access_token

                const headers = {
                    'Accept': 'application/json',
                    'Authorization': 'Bearer ' + accessToken,    
                }

                axios.get('http://laravel-api-server.test/api/test', { headers })
                    .then(({ data }) => {
                        console.log(data)
                    })
            })

    }
}
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
