<template>
  <div class="service-catalog">
    <div class="catalog-top">
      <div class="catalog-top-left">
        <h1 class="catalog-header">Services</h1>
        <input
          v-model="searchQuery"
          class="search-input"
          placeholder="Search services"
        >
      </div>
      <AddNewServiceButton class="AddNewServiceButton" />
    </div>
    <ul
      class="catalog"
    >
      <li
        v-for="service in services"
        :key="service.id"
        class="service"
      >
        <div>
          <ServiceCard :name="service.name" :description="service.description" />
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import useServices from '@/composables/useServices'
import AddNewServiceButton from '@/components/AddNewServiceButton.vue'
import ServiceCard from '@/components/ServiceCard.vue'

export default defineComponent({
  name: 'ServiceCatalog',
  setup() {
    // Import services from the composable
    const { services, loading } = useServices()

    // Set the search string to a Vue ref
    const searchQuery = ref('')

    return {
      services,
      loading,
      searchQuery,
      AddNewServiceButton,
      ServiceCard,
    }
  },
  components: {
    AddNewServiceButton,
    ServiceCard,
  },
})
</script>

<style lang="scss" scoped>
.service-catalog {
  max-width: 1366px;
  margin: 2rem auto;
  padding: 0 20px;
}

.catalog {
  display: flex;
  flex-wrap: wrap;
  margin: 20px 0 0 0;
  list-style: none;
}

.service {
  width: 200px;
  margin: 6px;
  border: 1px solid #999;
  border-radius: 10px;
  padding: 8px 16px;

  p:first-of-type {
    color: #333;
    font-weight: 700;
  }

  p {
    color: #666;
  }
}

.catalog-header {
  width: 127.57px;
  height: 28px;
  font-size: 24px;
  
  /* blue-700 */
  color: #0A2B66;
}

.search-input {
  margin: auto;
}

.catalog-top {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 18px 46px;
  max-width: 1216px;
}

.catalog-top-left {
  display: flex;
  flex-direction: column;
  align-items: left;
}

.AddNewServiceButton {
  margin: inherit;
}

input {
  padding: 8px 4px;
}
</style>
