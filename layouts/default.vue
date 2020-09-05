<template>
  <v-app>
    <v-app-bar app clipped-right dense color="#ffc107">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Weather app</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" app color="secondary">
      <v-list dense>
        <v-list-item>
          <v-flex xs12 my-2>
            <nuxt-link to="/" black--text>Home</nuxt-link>
          </v-flex>
        </v-list-item>
        <v-list-item @click.stop="left = !left">
          <v-flex xs12 my-2>
            <nuxt-link to="/myTables" black--text> My citys</nuxt-link>
          </v-flex>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main color="secondary">
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    drawerRight: null,
    right: false,
    left: false,
  }),
}
</script>

<style lang="css">
main {
  background-color: #fff59d;
}
a {
  color: black !important;
  text-decoration: none;
}
</style>
