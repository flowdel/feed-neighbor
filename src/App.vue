<template>
    <div id="app">
        <app-header />
        <router-view />
    </div>
</template>

<script>
import Header from './components/header/Header.vue';
import store from './store/store';
import { getIdToken, getUserId } from './storage';

export default {
    name: 'App',
    components: {
        appHeader: Header,
    },
    data() {
        return {
            test: 'pepe',
        };
    },
    async created() {
        const idToken = await getIdToken();
        const userId = await getUserId();

        await store.dispatch('tryAutoLogin', {
            idToken,
            userId,
        });
    },
    // async beforeRouteEnter(to, from, next) {
    // const idToken = await getIdToken();
    // const userId = await getUserId();
    // console.log(`app-beforerouteenter ${idToken}`);
    // next(() => {
    //     store.dispatch('tryAutoLogin', {
    //         idToken,
    //         userId,
    //     });
    // });

    //     next((vm) => {
    //         // eslint-disable-next-line no-param-reassign
    //         vm.test = 123;
    //     });
    // },
    // async created() {
    //     const idToken = await getIdToken();
    //     const userId = await getUserId();
    //     this.$store.dispatch('tryAutoLogin', {
    //         idToken,
    //         userId,
    //     });
    // },
};
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

  *,
  *::before,
  *::after {
      box-sizing: border-box;
  }

  *:focus {
    outline: 0;
  }

  body {
    font-family: 'Roboto', sans-serif;
    font-weight: 400;
    font-size: 16px;
    color: #333131;
    margin: 0;
  }

  img {
    max-width: 100%;
  }

  .container {
    width: 100%;
    padding-right: 15px;
    padding-left: 15px;
  }

  .spacer {
    height: 1px;
    margin-bottom: 15px;
  }

  .headline {
    font-size: 22px;
    margin-bottom: 15px;
  }

  .form-group {
    margin-bottom: 10px;
  }
</style>
