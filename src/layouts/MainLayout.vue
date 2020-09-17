<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <div class="q-px-lg q-pt-xl q-mb-xl">
        <div class="text-h3">Tarefas</div>
        <div class="text-subtitle"> {{ todayF }}</div>
      </div>
      <q-img src="~assets/mountains.jpg"
        class="header-image absolute-top"/>
    </q-header>
    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'

export default {
  name: 'MainLayout',
  computed: {
    todayF () {
      const timeStamp = Date.now()
      const formattedString = date.formatDate(timeStamp, 'dddd, DD/MM/YYYY ')
      return formattedString
    }
  }
}
</script>

<style lang="scss">
  .header-image {
    height: 100%;
    z-index: -1;
    opacity: 0.4;
    filter: grayscale(70%);
  }
</style>
