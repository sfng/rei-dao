<template>
  <v-app dark>
    <nav-header />
    <side-menu />
    <v-main class="grey" :class="dark ? 'darken-3' : 'lighten-3'">
      <router-view />
    </v-main>
    <bottom-nav />
  </v-app>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';
import NavHeader from './components/NavHeader';
import SideMenu from './components/SideMenu';
import BottomNav from './components/BottomNav';

export default {
  name: 'App',
  components: {
    NavHeader,
    SideMenu,
    BottomNav
  },
  computed: {
    ...mapGetters({
      dark: 'dark',
      darkMode: 'darkMode'
    })
  },
  mounted() {
    let media = window.matchMedia('(prefers-color-scheme: dark)');
    if (media) {
      media.onchange = (event) => {
        console.log(event.matches);
        if (this.darkMode == 2 && this.dark != event.matches) {
          this.switchDarkMode({ darkMode: 0 });
          this.switchDarkMode({ darkMode: 2 });
        }
      };
    }
    this.switchDarkMode({ darkMode: Number(localStorage.getItem('darkMode') || '2') });
  },
  methods: {
    ...mapActions({
      switchDarkMode: 'switchDarkMode'
    })
  }
};
</script>
<style>
@font-face {
  font-family: Bebas-Regular;
  src: url(./assets/fonts/Bebas-Regular.ttf);
  font-weight: 400;
  font-style: normal;
}

.bebas {
  font-family: Bebas-Regular;
}
</style>
