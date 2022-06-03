<template>
  
  <ServiceCatalog />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import ServiceCatalog from '@/components/ServiceCatalog.vue'
import AddNewServiceButton from '@/components/AddNewServiceButton.vue'

export default defineComponent({
  name: 'PageHome',
  components: {
    ServiceCatalog,
    AddNewServiceButton,
  },
})
</script>
