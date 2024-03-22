<template>
    <div class="background">
      <div class="players-page">
        <div class="card">
          <DataTable :value="players" :paginator="true" :rows="4" dataKey="id" :filters.sync="filters" filterDisplay="menu" :loading="loading" responsiveLayout="scroll"
              :globalFilterFields="['first_name', 'last_name', 'ranking', 'country']">
            <template #header>
              <div class="flex justify-content-between">
                <Button type="button" icon="pi pi-filter-slash" label="Clear" class="p-button-outlined" @click="clearFilter"/>
                <span class="p-input-icon-left">
                  <i class="pi pi-search" />
                  <InputText v-model="filters['global'].value" placeholder="Recherche par mot-clé" />
                </span>
              </div>
            </template>
            <template #empty>
              No players found.
            </template>
            <template #loading>
              Loading players data. Please wait.
            </template>
            <Column field="first_name" header="Prénom" :styles="{'min-width':'12rem'}" sortable>
              <template #body="{data}">
                <div>{{ data.first_name }}</div>
              </template>
              <template #filter="{filterModel}">
                <InputText type="text" v-model="filterModel.value" class="p-column-filter" placeholder="Search by first name"/>
              </template>
            </Column>
            <Column field="last_name" header="Nom" :styles="{'min-width':'12rem'}" sortable>
              <template #body="{data}">
                <div>{{ data.last_name }}</div>
              </template>
              <template #filter="{filterModel}">
                <InputText type="text" v-model="filterModel.value" class="p-column-filter" placeholder="Search by last name"/>
              </template>
            </Column>
            <Column field="country" header="Pays" :styles="{'min-width':'12rem'}" sortable>
              <template #body="{data}">
                <div>{{ data.country }}</div>
              </template>
              <template #filter="{filterModel}">
                <InputText type="text" v-model="filterModel.value" class="p-column-filter" placeholder="Search by country"/>
              </template>
            </Column>
            <Column header="Profil" :styles="{'min-width':'8rem'}">
              <template #body="{data}">
                <router-link :to="`/players/${data.slug}`" class="profile">Voir le Profil</router-link>
              </template>
            </Column>
          </DataTable>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, onMounted, Vue } from 'vue';
  import DataTable from 'primevue/datatable';
  import Column from 'primevue/column';
  import InputText from 'primevue/inputtext';
  import { FilterMatchMode, FilterOperator } from 'primevue/api';
  import Button from 'primevue/button';
  
  export default {
    components: {
      DataTable,
      Column,
      Button,
      InputText
    },
    data() {
      return {
        filters: {
          global: { value: null, matchMode: FilterMatchMode.CONTAINS },
          ranking: { value: null, matchMode: FilterMatchMode.STARTS_WITH },
          first_name: { value: null, matchMode: FilterMatchMode.STARTS_WITH },
          last_name: { value: null, matchMode: FilterMatchMode.STARTS_WITH },
          country: { value: null, matchMode: FilterMatchMode.STARTS_WITH }
        },
        players: []
      };
    },
    methods: {
      clearFilter() {
        this.filters = {
          global: { value: null, matchMode: FilterMatchMode.CONTAINS },
          ranking: { value: null, matchMode: FilterMatchMode.STARTS_WITH },
          first_name: { value: null, matchMode: FilterMatchMode.STARTS_WITH },
          last_name: { value: null, matchMode: FilterMatchMode.STARTS_WITH },
          country: { value: null, matchMode: FilterMatchMode.STARTS_WITH }
        };
      }
    },
    async asyncData({ $axios }) {
      try {
        const response = await $axios.get('/api/players');
        return { players: response.data.data || [] }; // Assurez-vous que cela renvoie toujours un tableau
      } catch (error) {
        console.error('Erreur lors de la récupération des joueurs:', error);
        return { players: [] }; // Retournez un tableau vide en cas d'erreur
      }
    }
  }
  </script>
  
  <style>
  .background {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-image: url("assets/terrain-de-basket.jpg");
    background-size: cover;
  }
  
  .players-page {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
  }
  
  .card {
    background-color: rgba(255, 255, 255, 0.8);
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}

.p-datatable {
  width: 100%;
}

.p-datatable .p-datatable-thead > tr > th {
  text-align: center;
  vertical-align: middle;
}

.p-datatable .p-datatable-tbody > tr > td {
  text-align: center;
  vertical-align: middle;
}

.profile {
  position: relative;
  text-decoration: none;
  color: black;
  font-weight: bold;
  padding: 5px 10px;
  border-radius: 5px;
  transition: all 0.3s ease-in-out;
}

.profile::before {
  content: '';
  background: black;
  display: block;
  position: absolute;
  bottom: -3px;
  left: 0;
  width: 0;
  height: 2px;
  transition: all 0.3s ease-in-out;
}

.profile:hover::before {
  width: 100%;
}
</style>

  