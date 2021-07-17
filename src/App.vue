<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app :mobile-breakpoint="768">
      <v-img
          height="170"
          src="mountains.jpg"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
          class="pa-4 pt-7"
      >
        <v-avatar size="70" class="mb-2">
          <img
              src="https://s.gravatar.com/avatar/4357e03f649d1d375b621c0aa90643e3?s=80"
              alt="Stas"

          >
        </v-avatar>
        <div class="text-subtitle-1 white--text font-weight-bold">
          Stas Tismenetski
        </div>
        <div class="text-subtitle-2 white--text">
          User_Stas
        </div>
      </v-img>


      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link :to="item.to">
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
        app
        color="primary"
        dark
        src="mountains.jpg"
        prominent
        :height="$route.path==='/' ? '238' : '170'">
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
        ></v-img>
      </template>

      <v-container class="pa-0 header-container">
      <v-row>
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
        <v-spacer></v-spacer>
        <search></search>
      </v-row>
        <v-row><v-app-bar-title class="text-h4 ml-4">{{$store.state.appTitle}}</v-app-bar-title></v-row>
     <v-row>
    <live-date-time></live-date-time>
     </v-row>
        <v-row v-if="$route.path === '/'">
          <field-add-task></field-add-task>
        </v-row>
      </v-container>
    </v-app-bar>
    <v-main>
      <router-view></router-view>
      <snackbar></snackbar>
    </v-main>
  </v-app>
</template>

<script>
import Snackbar from "./components/Shared/Snackbar";
import Search from "./components/Tools/Search";
import LiveDateTime from "./components/Tools/LiveDateTime";
import FieldAddTask from "./components/Todo/FieldAddTask";
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
      { title: 'About', icon: 'mdi-help-box', to: '/about' },
    ],
  }),


  components : {
    Snackbar,
    Search,
    LiveDateTime,
    FieldAddTask
  },
  mounted() {
    this.$store.dispatch('getTasks');
  }
};
</script>

<style lang="sass">

.header-container
  max-width: none !important

</style>