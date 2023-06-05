<template>
  <div class="catalog-filter">
    <div><input type="checkbox" v-model="formParams.hasBreed" /> hasBreed</div>

    <select v-model="formParams.selectedBreeds">
      <option v-for="breed in breedsOptions" :value="breed.id">{{ breed.label }}</option>
    </select>
  </div>
</template>

<script lang="js">
  import CatCard from '@/components/CatCard.vue';

  export default {
    name: 'CatalogFilter',

    components: {
      CatCard
    },

    created() {
      this.getBreeds()
    },

    data: () => ({
      formParams: {
        selectedBreeds: null,
        hasBreed: false
      },

      breeds: [],
      selectedBreeds: null
    }),



    computed: {
      breedsOptions() {
        return this.breeds.map(i => ({
          id: i.id,
          label: i.name
        }))
      }
    },

    methods: {
      async getBreeds() {
        try {
          const responce = await fetch(`https://api.thecatapi.com/v1/breeds`, {
            headers: {
              'x-api-key': "live_7xtMA7fut6rmEc4gbJDaNLztQ6WdCCA3NpcbAwuD6faYohJHAf1zGKoyL3MLNwXQ",
            },
          })

          const breeds = await responce.json()

          this.breeds = breeds
        } catch (e) {

        }
      },
    },

    watch: {
      formParams: {
        handler(value) {
          this.$emit('recalc', {...value})
        },
        deep: true,
        
      }
    }
  }
</script>

<style lang="scss">
  .catalog {
    padding: 50px 0;
  }
</style>
