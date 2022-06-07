<template>
  <header>
    <div class="nav">
      <router-link to="/">
        KONNECT
      </router-link>
      <div class="nav-icons">
        <KIcon icon="notificationBell" style="padding: 14px;"/>
        <KIcon icon="info" size="24" style="padding: 14px;"/>
        <KIcon icon="profile" size="30" style="padding: 14px;"/>
        </div>
      
    </div>
  </header>
  <main>
    <RouterView />
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { RouterView } from 'vue-router'
import { KIcon } from '@kong/kongponents'

export default defineComponent({
  name: 'App',
  components: { 
    RouterView, 
    KIcon 
  },
})
</script>

<style lang="scss">
html {
  margin: 0;
  padding: 0;
  font-size: 10px;
}

body {
  font-family: Arial, sans-serif;
  font-weight: 400;
  font-size: 1.6rem;
  line-height: 1.2;
  margin: 0 auto;
}

.nav {
  padding: 16px;
  margin-bottom: 4rem;
  border-bottom: 1px solid #333;
  display: flex;
  justify-content: space-between;

  a {
    font-weight: 700;
    color: blue;

    &.router-link-exact-active {
      color: #0A2B66;
      text-decoration: none;
      font-size: 3rem;
    }
  }
}

.nav-icons {
  padding: 0 36px;
}
</style>
