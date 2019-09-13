<template>
  <v-app>
   <nav> 
    <v-app-bar app dark>
      <v-app-bar-nav-icon depressed class="white--text" @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light">Monster</span>
        <span class="font-weight-heavy">Project</span>
      </v-toolbar-title>
    </v-app-bar>
  <v-navigation-drawer v-model="drawer" app dark class="white--text">
    <v-list dark rounded>
      <v-list-item-group  class="title">
        <v-list-item> {{ Home }} </v-list-item>
        <v-list-item> {{ About }} </v-list-item>
      </v-list-item-group>
    </v-list>
  </v-navigation-drawer>

   </nav>

    <v-content>
      <monster/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import monster from './components/monster';
import { VApp, VAppBar, VToolbarTitle, VContent, VBtn, VNavigationDrawer, VAppBarNavIcon, VList, VListItem, VListItemGroup} from 'vuetify/lib'


export default {
  name: 'App',
  components: {
    HelloWorld,
    monster,
    VApp,
    VAppBar,
    VToolbarTitle,
    VContent,
    VBtn,
    VNavigationDrawer,
    VAppBarNavIcon,
    VList,
    VListItem,
    VListItemGroup
  },
  data: () => ({
    drawer: false,
    Home: 'Home',
    About: 'About'
  }),
};

</script>
