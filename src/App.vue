<template>
    <div id="app" class="container">
        <img src="./assets/logo.png">
        <div class="router-links">
            <router-link class="router-link" to="/without-vuex">Крестики-нолики без vuex</router-link>
            <router-link class="router-link" to="/with-vuex">Крестики-нолики c vuex</router-link>
            <router-link class="router-link" to="/excel">Excel</router-link>
        </div>
        <HelloWorld
                msg="Welcome to Tic-Tac game!"/>
        <router-view></router-view>
    </div>
</template>

<script>
    import HelloWorld from '@/components/HelloWorld.vue'
    import Vue from 'vue';
    import VueRouter from 'vue-router';
    import TicTacGame from '@/components/without-vuex/TicTacGame'
    import TicTacGame2 from '@/components/with-vuex/TicTacGame2'
    import ExcelWrap from '@/components/excel/ExcelWrap'

    /*-------------------Router ---------------*/

    Vue.use(VueRouter);

    const routes = [
        {path: '/without-vuex', component: TicTacGame},
        {path: '/with-vuex', component: TicTacGame2},
        {path: '/excel', component: ExcelWrap}
    ];

    const router = new VueRouter({
        routes // сокращённая запись для `routes: routes`
    });

    /*-------------------Store------------------*/



    export default {
        router,
        name: 'app',
        components: {
            HelloWorld,
            TicTacGame,
            TicTacGame2,
            ExcelWrap
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
        margin-top: 1vh;
    }
    .container img[src*="logo"] {
        display: block;
        margin: 0 auto 15px;
        max-width: 100px;
    }

    .router-links {
        display: flex;
        justify-content: center;
        width: 100%;
    }
    .router-link {
        margin: 0 10px;
        display: inline-block;
        padding: 10px;
        background: #41b883;
        opacity: .6;
        text-decoration: none;
        text-transform: uppercase;
        color: #fff;
    }
    .router-link:hover {
        opacity: 1;
    }
</style>
