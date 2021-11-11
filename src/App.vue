<template>
  <v-app id="inspire" v-on:log-me-in="loggedIn = !loggedIn">
    <div v-if="!loggedIn"></div>
    <div v-if="loggedIn">
      <v-navigation-drawer v-model="drawer" app>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="title"> Remind RX </v-list-item-title>
            <v-list-item-subtitle>
              A Better Life for Patients
            </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider>

        <v-list dense nav>
          <v-list-item
            v-for="item in items"
            :key="item.title"
            :to="item.to"
            link
          >
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-app-bar app dark color="primary" src="water.jpg">
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

        <v-toolbar-title>Remind RX</v-toolbar-title>
        <v-text-field
          class="mt-2 mx-7"
          label="Search for patients"
          append-outer-icon="mdi-magnify"
          clearable
        ></v-text-field>
        <v-spacer></v-spacer>

        <v-badge
          avatar
          overlap
          bottom
          bordered
          offset-y="18"
          offset-x="15"
          color="green"
          icon="mdi-check"
        >
          <v-avatar>
            <img src="doctor.jpg" alt="The big coof" />
          </v-avatar>
        </v-badge>
        <v-btn plain class="mt-2" to="login">
          Dr. Wheeler
          <v-icon>mdi-chevron-down</v-icon>
        </v-btn>
      </v-app-bar>
    </div>
    <v-main>
      <router-view v-on:log-me-in="loggedIn = !loggedIn"></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
    loggedIn: true,
    items: [
      { title: "Dashboard", icon: "mdi-home", to: "/" },
      { title: "Patients", icon: "mdi-account", to: "/" },
      { title: "Settings", icon: "mdi-cog", to: "/about" },
    ],
  }),
};
</script>
