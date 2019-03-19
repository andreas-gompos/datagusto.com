<template>
  <v-app light>
    <v-navigation-drawer
      v-model="drawer"
      temporary
      app
    >
      <v-toolbar>
        <v-toolbar-side-icon @click="drawer = !drawer"></v-toolbar-side-icon>
        <v-toolbar-title class="blue--text text--darken-2" @click="drawer = !drawer">
          <nuxt-link to="/" tag="span" style="cursor: pointer">Datagusto</nuxt-link>
        </v-toolbar-title>
      </v-toolbar>

      <v-divider></v-divider>
      <v-list>
        <v-list-tile
          v-for="(item, i) in items"
          :to="item.to"
          :key="i"
        >
          <v-list-tile-action>
            <v-icon v-html="item.icon" />
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title" />
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      fixed
      app
    >
      <v-toolbar-side-icon class="hidden-sm-and-up"@click="drawer = !drawer" />

      <v-toolbar-title class="blue--text text--darken-2">
          <nuxt-link to="/" tag="span" style="cursor: pointer">{{title}}</nuxt-link>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-xs-only">
            <v-btn
                color="blue darken-1"
                 flat
                v-for="menuItem in items"
                :key="menuItem.title"
                :to="menuItem.to">
                <v-icon left>{{ menuItem.icon }}</v-icon>
                {{menuItem.title}}
            </v-btn>
      </v-toolbar-items>
    </v-toolbar>

    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer
      :fixed="fixed"
      app
    >
      <v-spacer></v-spacer>
      <span>&copy;Datagusto 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    data() {
      return {
        drawer: false,
        fixed: false,
        items: [
          { icon: 'bubble_chart', title: 'Models', to: '/models' },
          { icon: 'library_books', title: 'Blog', to: '/blog' },
          { icon: 'info', title: 'About', to: '/about' }
        ],
        title: 'Datagusto'
      }
    }
  }
</script>
