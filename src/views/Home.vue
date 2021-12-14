<template>
  <div class="min-h-screen w-full bg-gray-900 text-gray-300 flex flex-col items-center">
    <div class="">
    <h1 class="text-6xl font-semibold pt-32 pb-12">Crypto Plateform</h1>
    <CoinTable />
    </div>
  </div>
</template>

<script>

import CoinTable from '../components/coinTable.vue';
// @ is an alias to /src

export default {
  name: 'Home',
  data () {
    return {

    }
  },
  components: {
    CoinTable
  },
  methods: {
  },
  computed: {

  },
 
}
</script>
