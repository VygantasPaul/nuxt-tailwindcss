<template>
  <div>
    <div class="row justify-center">
      <div class="w-full md:w-8/12 lg:w-4/12 pb-5">
        <button @click="$fetch" class="btn btn-blue text-left bg-bg-blue-500 hover:bg-blue-700  hover:underline">Refresh</button>
      </div>
    </div>

    <div class="row justify-center">
      <div class="w-full md:w-8/12 lg:w-4/12">
        <p v-if="$fetchState.pending">Loading mountains....</p>
        <p v-else-if="$fetchState.error">Error while fetching mountains</p>
      </div>
    </div>
    <div class="row justify-center">
      <div class="w-full md:w-8/12 lg:w-4/12 pb-5" v-for="mountain in mountains" :key="mountain.title" v-if="mountains.length">
        <div class="mx-4 bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700">
          <img class="rounded-t-lg" :src="mountain.image" :alt="mountain.title">
          <div class="p-5">
            <NuxtLink :to="`/posts/${mountain.slug}`">
              <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{ mountain.title }}</h5>
            </NuxtLink>
            <div class="pb-3">
              <span class="bg-blue-100 text-blue-800 text-sm font-medium mr-2 px-2.5 py-0.5 rounded dark:bg-blue-200 dark:text-blue-800 ">{{ mountain.updatedAt }}</span>
            </div>

            <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">{{ mountain.description }}</p>
            <NuxtLink :to="`/posts/${mountain.slug}`" class="inline-flex items-center py-2 px-3 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
              Read more
              <svg aria-hidden="true" class="ml-2 -mr-1 w-4 h-4" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"></path>
              </svg>
            </NuxtLink>
          </div>
        </div>
      </div>
      <div v-else>No mountains available</div>

    </div>
  </div>
</template>

<script>

export default {

  async fetch() {
    this.mountains = await fetch('http://api.nuxtjs.dev/mountains').then((res) => res.json())
  },
  data() {
    return {
      mountains: []
    }

  }
}
</script>

<style lang="postcss">
.border-btn {
  background-color: transparent;
  --tw-border-opacity: 1;
  border-color: rgba(88, 100, 255, var(--tw-border-opacity));
  border-style: solid;
  border-width: 2px;
  --tw-text-opacity: 1;
  color: rgba(88, 100, 255, var(--tw-text-opacity));
}

.btn {
  @apply font-bold py-2 px-4 rounded;
}

.btn-blue {
  @apply bg-blue-500 text-white;
}

.btn-blue:hover {
  @apply bg-blue-700;
}
</style>
