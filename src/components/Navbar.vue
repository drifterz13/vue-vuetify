<template>
  <nav>
    <v-snackbar :timeout="4000" v-model="snackbar" top color="success">
      <span>You've already added a new project.</span>
      <v-btn flat color="white" @click="snackbar = false">Close</v-btn>
    </v-snackbar>
    <v-navigation-drawer
      :permanent="drawer && $vuetify.breakpoint.mdAndUp"
      v-model="drawer"
      app
      class="primary"
    >
      <v-list>
        <v-layout column align-center>
          <v-flex class="mt-5">
            <v-avatar size="100">
              <img src="/avatar-1.png" alt="user-avatar">
            </v-avatar>
            <p class="subheading white--text mt-1">The net ninja</p>
          </v-flex>
          <v-flex class="mt-4 mb-3">
            <pop-up v-on:created-new-project="snackbar = true"></pop-up>
          </v-flex>
        </v-layout>
        <v-list-tile v-for="list in lists" :key="list.icon" router :to="list.route">
          <v-list-tile-action>
            <v-icon class="white--text">{{ list.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title class="white--text">{{ list.text }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>

    <v-toolbar app flat>
      <v-toolbar-side-icon class="grey--text" @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="text-uppercase grey--text">
        <span class="font-weight-light">Todo</span>
        <span>Ninja</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>

      <v-menu offset-y :hidden="$vuetify.breakpoint.smAndDown">
        <v-btn slot="activator" color="grey" flat>
          <v-icon left>expand_more</v-icon>
          <span>Menu</span>
        </v-btn>
        <v-list>
          <v-list-tile v-for="list in lists" :key="list.icon" router :to="list.route">
            <v-list-tile-title>{{ list.text }}</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>

      <v-btn flat color="grey">
        <span>Sign out</span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn>
    </v-toolbar>
  </nav>
</template>

<script>
import Popup from "./Popup";

export default {
  components: {
    "pop-up": Popup
  },
  data() {
    return {
      drawer: false,
      snackbar: false,
      lists: [
        {
          icon: "dashboard",
          text: "Dashboard",
          route: "/"
        },
        {
          icon: "folder",
          text: "My Projects",
          route: "/projects"
        },
        {
          icon: "person",
          text: "Team",
          route: "/team"
        }
      ]
    };
  },
  methods: {}
};
</script>
