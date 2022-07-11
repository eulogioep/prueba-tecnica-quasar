<template>
<q-layout view="hHh lpR fFf">

    <q-header bordered class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title class="q-pt-sm">

            <img src="https://www.freetogame.com/assets/images/freetogame-logo.png">


        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'


export default defineComponent({
  name: 'MainLayout',

  components: {

  },

  setup () {


    return {

    }
  }
})
</script>
