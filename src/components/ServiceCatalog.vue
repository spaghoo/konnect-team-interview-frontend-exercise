<template>
  <div class="service-catalog">
    <div class="catalog-top">
      <div class="catalog-top-left">
        <h1 class="catalog-header">Services</h1>
        <input
          v-model="searchQuery"
          class="search-input"
          placeholder="Search"
        >
      </div>
      <AddNewServiceButton class="AddNewServiceButton" />
    </div>
    <div v-if="loading" class="loading">
      <h1 style="color: #0A2B66">DATA LOADING</h1>
      <KIcon icon="spinner" colo="#0A2B66" size="300" />
    </div>
    <div v-else>
      <div v-if="services.length != 0">
        <div v-if="searchServiceResults.length != 0">
            <ul
              class="catalog"
            >
              <li
                v-for="service in paginatedResults"
                :key="service.id"
                class="service"
              >
                <div>
                  <ServiceCard :name="service.name" :description="service.description" :versions="service.versions.length" />
                </div>
              </li>
            </ul>
        </div>
        <div v-else>
          <h2 style="color: #0A2B66; text-align: center">NO RESULTS TO YOUR QUERY</h2>
        </div>
      </div>
      <div v-else>
        <h2 style="color: #0A2B66; text-align: center">NO RESULTS TO YOUR API CALL</h2>
      </div>
    </div>
    <div class="pagination-row">
      <div v-if="pageNumber <= 1">
        <button
        class="pagination-button"
        v-on:click.native="changePage(pageNumber - 1)" 
        v-bind:disabled="pageNumber <= 1"><KIcon icon="arrowLeft" color="grey" /></button>
      </div>
      <div v-else>
        <button
        class="pagination-button"
        v-on:click.native="changePage(pageNumber - 1)" 
        v-bind:disabled="pageNumber <= 1"><KIcon icon="arrowLeft" color="#1456CB" /></button>
      </div>
      <PaginationNumbers
        :currentPage="pageNumber"
        :maxPages="getMaxPages"
        :itemsPerPage="this.itemsPerPage"
        :totalItems="searchServiceResults.length -1" />
      <div v-if="pageNumber >= getMaxPages">
        <button
        class="pagination-button"
        v-on:click.native="changePage(pageNumber + 1)" 
        v-bind:disabled="pageNumber >= getMaxPages"><KIcon icon="arrowRight" color="grey" /></button>
      </div>
      <div v-else>
        <button
        class="pagination-button"
        v-on:click.native="changePage(pageNumber + 1)" 
        v-bind:disabled="pageNumber >= getMaxPages"><KIcon icon="arrowRight" color="#1456CB" /></button>
      </div>
    </div>
  </div>
  
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import useServices from '@/composables/useServices'
import AddNewServiceButton from '@/components/AddNewServiceButton.vue'
import ServiceCard from '@/components/ServiceCard.vue'
import PaginationNumbers from '@/components/PaginationNumbers.vue'
import { KIcon } from '@kong/kongponents'

export default defineComponent({
  name: 'ServiceCatalog',
  setup() {
    // Import services from the composable
    const { services, loading } = useServices()

    // Set the search string to a Vue ref
    
    const pageNumber = ref(1)
    const debouncedInput = ref('')
    const passedTimeout = 300
    const itemsPerPage = 12
    const storedPageNumber = ref(0)
    const justSearched = ref(true)

    return {
      services,
      loading,
      pageNumber,
      debouncedInput,
      passedTimeout,
      itemsPerPage,
      storedPageNumber,
      justSearched
    }
  },
  components: {
    AddNewServiceButton,
    ServiceCard,
    PaginationNumbers,
    KIcon
  },
  methods: {
    changePage(page) {
      this.pageNumber = page;
    },
  },
  computed: {
    searchQuery: {
      get() {
        return this.debouncedInput
      },
      set(passedValue) {
        if (this.timeout) clearTimeout(this.timeout)
          this.timeout = setTimeout(() => {
            this.debouncedInput = passedValue
          }, this.passedTimeout)
        }
    },
    searchServiceResults: function () {
        var localServices = this.services;
        
        var localSearchQuery = this.searchQuery
        
        //doesnt run the search if nothing is in the search bar or if only one letter is
        
        if(!localSearchQuery || localSearchQuery.length < 2){
          if (this.storedPageNumber != 0) {
              this.justSearched = !this.justSearched
              this.pageNumber = this.storedPageNumber
          }
          return localServices
        }
        //trims to lowercase for case insensitive search
        var localSearchQuery = localSearchQuery.trim().toLowerCase();
        
        
        if (this.justSearched) {
            this.storedPageNumber = this.pageNumber
            this.pageNumber = 1;
            this.justSearched = !this.justSearched
        }
        
        localServices = localServices.filter(function(item){
          if(item.name.toLowerCase().indexOf(localSearchQuery) !== -1){
            return item
          }
        })
        
        return localServices
    },
    paginatedResults: function () {;
      return this.searchServiceResults.slice(this.getCurrentSlice-this.itemsPerPage,this.getCurrentSlice);
    },
    getCurrentSlice: function () {
        return this.pageNumber * this.itemsPerPage;
    },
    getMaxPages: function () {
        if (this.debouncedInput.length > 0) {
            let maxNum = this.searchServiceResults.length / this.itemsPerPage
            return Math.ceil(maxNum)
        }
        let maxNum = this.services.length / this.itemsPerPage
        return Math.ceil(maxNum)
    }
  },
})
</script>

<style lang="scss" scoped>
.service-catalog {
  max-width: 1250px;
  margin: 2rem auto;
  padding: 0 20px;
}
.pagination-row {
  padding: 20px 0px;
  display: flex;
  justify-content: space-around
}
.pagination-button {
  background-color: white;
  border-radius: 50%;
  border: 1px solid #1456CB;
  padding: 10px;
}
.pagination-button:disabled {
  background-color: white;
  border-radius: 50%;
  border: 1px solid grey;
  padding: 10px;
}

.catalog {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 20px 20px 0 0;
  list-style: none;
}

.service {
  width: 250px;
  height: 240px;
  margin: 6px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 5px;
  padding: 8px 16px;

  p:first-of-type {
    color: #333;
    font-weight: 700;
  }

  p {
    color: #666;
  }
}

.service:hover {
  border: 1px solid rgba(166, 198, 255, 1);
}

.catalog-header {
  width: 127.57px;
  height: 28px;
  font-size: 30px;
  
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
  display: block;
  width: 195px;
  padding: 10px 45px;
  background: url("../images/searchIcon.svg") no-repeat 15px center;
  background-size: 15px 15px;
  font-size: 16px;
  border: grey solid 1px;
}
.loading {
  text-align: center;
}
</style>
