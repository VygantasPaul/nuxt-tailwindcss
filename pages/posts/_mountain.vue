<template>
  <div>
    <div class="container mx-auto text-center">
      <div class="justify-center row text-center">
        <div class="w-full pb-5">
          <Nuxt-link to="/posts" class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded">Go back</Nuxt-link>
        </div>

        <div class="w-full md:w-8/12 lg:w-4/12  bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700 ">
          <img class="rounded-t-lg mx-auto" :src="details.image" :alt="details.title">

          <div class="p-4">
            <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{ details.title }}</h5>
            <div class="pb-3">
              <span>Height:</span> <span class="bg-yellow-100 text-yellow-800 text-sm font-medium mr-2 px-2.5 py-0.5 rounded dark:bg-blue-200 dark:text-blue-800">{{ details.height }}</span>
            </div>
            <div class="pb-3">
              <span>Continent:</span> <span class="bg-pink-100 text-pink-800 text-sm font-medium mr-2 px-2.5 py-0.5 rounded dark:bg-pink-200 dark:text-pink-900">{{ details.continent }}</span>
            </div>
            <div class="pb-3">
              <span>Country:</span> <span class="bg-indigo-100 text-indigo-800 text-sm font-medium mr-2 px-2.5 py-0.5 rounded dark:bg-indigo-200 dark:text-indigo-900" v-for="country in details.countries" :key="country">{{country}}</span>
            </div>
            <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">{{ details.description }}</p>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      details: {},
    }
  },
  async fetch() {
    const response = await fetch(`https://api.nuxtjs.dev/mountains/${this.$route.params.mountain}`)
    this.details = await response.json()
  },
}
</script>

<style scoped>

</style>
