<template>
  <v-app>
   <nav> 
    <v-app-bar app dark>
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light white--text">Monster</span>
        <span class="font-weight-heavy white--text">Project</span>
      </v-toolbar-title>
    </v-app-bar>
   </nav>

    <v-content>
      <monster/>
    </v-content>
    
  </v-app>
</template>

<script>
import monster from './components/monster';
import { VApp, VAppBar, VToolbarTitle, VContent, VBtn, VNavigationDrawer, VAppBarNavIcon, VList, VListItem, VListItemGroup} from 'vuetify/lib'


export default {
  name: 'App',
  components: {
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
