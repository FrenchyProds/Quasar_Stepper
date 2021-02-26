<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-grey-1" elevated>
      <q-toolbar>
        <q-btn
          style="color: #A9A9A9;"
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
        <q-btn
          style="color: #A9A9A9;"
          flat
          dense
          round
          icon="refresh"
        />
        <q-btn
          style="color: #A9A9A9;"
          flat
          dense
          round
          icon="cancel"
          @click="step = 1"
        />
      </q-toolbar>
    </q-header>
    
    <q-drawer
      v-if(leftDrawerOpen)
      v-model="leftDrawerOpen"
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
          Random Info
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'

const linksData = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/FrenchyProds',
    icon: 'code',
    link: 'https://github.com/FrenchyProds'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
];

export default {
  name: 'MainLayout',
  components: { EssentialLink },
  data () {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData
    }
  }
}
</script>
