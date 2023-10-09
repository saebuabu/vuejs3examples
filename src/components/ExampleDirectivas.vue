<template>
    <h1>Netflix Streaming service</h1>  
    <section v-if="loggedIn">
        <p>Watch your movies || Your age : <input size="2" type="number" v-model="user.age"></p>
        <ul v-if="user.age > 16">
            <li v-for="(movie,key) in movies" :key="key">
                    {{ movie.title }} - {{ movie.age }}
            </li>
        </ul>
        <ul v-else-if="user.age > 12 && user.age <= 16">
            <li v-for="(movie,key) in moviesJovenes" :key="key">
                    {{ movie.title }}  - {{ movie.age }}
            </li>
        </ul>
        <ul v-else>
            <li v-for="(movie,key) in moviesNinos" :key="key">
                    {{ movie.title }} - {{ movie.age }}
            </li>
        </ul>

        <!-- make an example with :class and the variable subscription -->
        <p :class="subscription">Your subscrption: {{ subscription }}</p>
        <button @click="logOut">Log out</button>

    </section>
    <section id="loginform" v-else>
        <p>Log in first:</p>
        <!-- make username and password fields with labels  and use v-model -->
        <input v-model="user.username" type="text" @keyup="resetLoginStatus" placeholder="username" />
        <input v-model="user.password" type="password" placeholder="password" />
        <!-- make a button with the text "Log in" -->
        <button @click="validateLogin">Log in</button>
        <p :class="loginstatus">Incorrect login, try again</p>
    </section>
</template>
<script lang="ts">

import { defineComponent } from 'vue';
import movies from '@/assets/films.json';

export default defineComponent ({
    data() {
        return {
            visible: true,
            loggedIn: false,
            subscription : 'gold',
            loginstatus: 'neutral',
            user: {
                username: '',
                password: '',
                age:  10
            }
        }
    },// add a computed function
    computed: {
        movies() {
            return movies;
        }, // make a function moviesJovenes that returns only movies with movie.age >12 && movie.age <= 16
        moviesJovenes() {
            return movies.filter(movie => movie.age <= 16);
        }, // make a function moviesNinos that returns only movies with movie.age <= 12
        moviesNinos() {
            return movies.filter(movie => movie.age <= 12);
        }
    },
    methods: {
        validateLogin() {
            if (this.user.username === 'admin' && this.user.password === 'admin') {
                this.loggedIn = true;
            }
            else {
                this.loginstatus = 'incorrect';
            }
        },
        logOut() {
            this.loggedIn = false;
        },
        resetLoginStatus() {
            this.loginstatus = 'neutral';
        }
    }
});

</script>

<style lang="scss">
    h1, section {
        margin: 0 auto 0 auto;
    }
    h1 {
        color: red;
    }
    .freemium {
        color: green;
    }
    .premium {
        color: blue;
    }
    .gold {
        color: gold;
    }
    p {
        font-size: 1.5rem;
    }
    #loginform {
        background-color: #ccc;
        padding: 20px;
        border-radius: 10px;
        width: 300px;
    }
    /* put each input field on a newline */
    #loginform input {
        margin: 10px;
        flex-grow: 4;
    }

    #loginform button {
        margin: 10px;
    }
    .neutral{
        display: none;
    }
    .incorrect {
        color: red;
    }

</style>