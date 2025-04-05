<template>
  <q-layout view="lHh Lpr lFf">
    <q-header >
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle">{{ todaysDate }}</div>
      </div>
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 190px); margin-top: 190px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item 
            exact
             to="/"
            clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                My Day
              </q-item-section>
            </q-item>

        
            <q-item
            to="/help"
             clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>

            
          </q-list>
        </q-scroll-area>

        <q-img class=" bg-primary  absolute-top"  style="height: 185px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="https://picsum.photos/200/400">
            </q-avatar>
            <div class="text-weight-bold">Naresh Gorle</div>
            <div>nareshgorle1@</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
      
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { date } from 'quasar'
import { ref,computed } from 'vue'



 
const todaysDate = computed(()=>{
  let timeStamp = Date.now()
return date. formattedString = date.formatDate(timeStamp, 'dddd D MMMM ')
})

const leftDrawerOpen = ref(false)

function toggleLeftDrawer () {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>
