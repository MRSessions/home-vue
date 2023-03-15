<template>
  <!-- <LogIn :dialog="loginDialog" @updateDialog="loginDialog = $event" /> -->
  <v-app-bar color="primary" prominent>
    <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

    <v-toolbar-title>{{ appStore.appSettings.name }}</v-toolbar-title>

    <v-spacer></v-spacer>

      <v-btn variant="text"
      :icon="appStore.appSettings.theme === 'dark' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
      @click="changeTheme"></v-btn>
      <v-btn variant="text"
      icon="mdi-cog-outline"></v-btn>
  </v-app-bar>

  <v-navigation-drawer color="drawer" v-model="drawer" :location="$vuetify.display.smAndDown ? 'top' : 'start'"
    :permanent="$vuetify.display.smAndDown ? false : true">
    <v-list>
      <v-list-item v-for="item in items" :key="item.title" :to="item.value">{{ item.title }}</v-list-item>
    </v-list>

    <!-- <template v-slot:append>
      <div class="pa-2">
        <v-btn block :color="authStore.authenticated ? 'error' : 'success'" @click="logInLogOut">
          {{ authStore.authenticated ? 'Logout' : 'Login' }}
        </v-btn>
      </div>
    </template> -->
</v-navigation-drawer>
</template>

<script setup lang="ts">

import vuetify from '@/plugins/vuetify';
import { ref, inject } from 'vue'
import { pocketBaseSymbol } from '@/pocketbase/injectionSymbols'
import { useAppStore } from '@/store/app';

// const pb = inject(pocketBaseSymbol)
const appStore = useAppStore()

const drawer = ref(!vuetify.display.smAndDown.value)
const items = ref([
  {
    title: 'Dashboard',
    value: '/dashboard',
  },
  // {
  //   title: 'About',
  //   value: '/about',
  // },
  // {
  //   title: 'Contact',
  //   value: '/contact',
  // },
])

function changeTheme() {
  appStore.appSettings.theme = appStore.appSettings.theme === 'dark' ? 'light' : 'dark'
}

</script>
