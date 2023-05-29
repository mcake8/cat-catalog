<template>
  <div class="catalog">
    <div class="container">
      <div class="row">
        <div class="col-xs-4" v-for="cat in cats">
          <cat-card class="mb-20" :src="cat.url" :width="cat.width" :height="cat.height" />
        </div>
      </div>

      {{ cats }}
    </div>
  </div>
</template>

<script lang="js">
  import CatCard from '@/components/CatCard.vue';
  import queryString from 'query-string';


  export default {
    name: 'Catalog',

    components: {
      CatCard
    },

    created() {
      this.getCats()
    },

    data: () => ({
      cats: [],
    }),

    methods: {
      async getCats() {

        const params = queryString.stringify({
          limit: 12,
          has_breeds: 1,
          order: 'ASC'
        })



        try {
          const responce = await fetch(`https://api.thecatapi.com/v1/images/search?${params}`, {
            headers: {
              'x-api-key': "live_7xtMA7fut6rmEc4gbJDaNLztQ6WdCCA3NpcbAwuD6faYohJHAf1zGKoyL3MLNwXQ",
            },
          })

          const cats = await responce.json()

          this.cats = cats
        } catch (e) {

        }
      }
    }
  }
</script>

<style lang="scss">
  .catalog {
    padding: 50px 0;
  }
</style>
