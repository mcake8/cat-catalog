<template>
  <div class="catalog">
    <div class="container">
      <catalog-filter @recalc="getCats" />

      <div class="row">
        <div class="col-xs-4" v-for="cat in cats">
          <cat-card class="mb-20" :src="cat.url" />
        </div>
      </div>

      {{ cats }}
    </div>
  </div>
</template>

<script lang="js">
  import CatCard from '@/components/CatCard.vue';
  import CatalogFilter from '@/components/CatalogFilter.vue'
  import queryString from 'query-string';

  export default {
    name: 'Catalog',

    components: {
      CatCard,
      CatalogFilter
    },

    created() {
      this.getCats()
    },

    data: () => ({
      cats: [],
    }),


    methods: {
      async getCats({selectedBreeds, hasBreed } = {}) {

        const params = {
          limit: 12,
          has_breeds: hasBreed,
          order: 'ASC'
        }

        if(selectedBreeds) {
          params.breed_ids = selectedBreeds
        }

        try {
          const responce = await fetch(`https://api.thecatapi.com/v1/images/search?${queryString.stringify(params)}`, {
            headers: {
              'x-api-key': "live_7xtMA7fut6rmEc4gbJDaNLztQ6WdCCA3NpcbAwuD6faYohJHAf1zGKoyL3MLNwXQ",
            },
          })

          const cats = await responce.json()

          this.cats = cats
        } catch (e) {

        }
      },


    }
  }
</script>

<style lang="scss">
  .catalog {
    padding: 50px 0;
  }
</style>
