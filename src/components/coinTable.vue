<template>
  <div v-if="allCoins" class="flex items-center justify-start min-h-screen bg-gray-900">
    <div class="col-span-12">
      <div class="overflow-auto lg:overflow-visible">
        <table class="table text-gray-400 border-separate space-y-6 text-xs">
          <thead class="bg-gray-800 text-gray-500">
            <tr class="border-1 border-gray-400">
              <th
                v-for="(head,name) in allCoins[0]"
                :key="name"
                class="px-3 py-2 text-left"
              >{{ name }}</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(row, index) in allCoins" :key="'ligne' + row.id + index" class="bg-gray-800">
              <td
                v-show="columnIndex === 0"
                v-for="(column, name, columnIndex) in row"
                :key="row.id + name + index"
                class="px-2 py-1"
              >{{ String(column).slice(0, 5) }}</td>
              <td
                v-show="columnIndex !== 0"
                v-for="(column, name, columnIndex) in row"
                :key="row.id + name + index"
                class="px-2 py-1"
                :class="name == 'reward' && column !== -1 && 'text-green-400'
                || name == 'price' && column !== -1 && 'text-red-400'
                || column == -1 && 'text-gray-700'"
              >{{ column }}</td>
              <!-- <td class="p-3 font-bold">200.00$</td>
              <td class="p-3">
                <span class="bg-green-400 text-gray-50 rounded-md px-2">available</span>
              </td>-->
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      allCoins: null,
    }
  },
  mounted () {
    const options = {
      method: 'GET',
      url: 'https://mineable-coins.p.rapidapi.com/coins',
      headers: {
        'x-rapidapi-host': 'mineable-coins.p.rapidapi.com',
        'x-rapidapi-key': 'HnP8swEtpJmshNmLqREFChlkWsmDp1sk5hZjsn9rkWt6k5fx8c'
      }
    };
    axios.request(options)
      .then(response => this.allCoins = response.data)
      .catch(function (error) {
        console.error(error);
      });
  }
}
</script>

<style>
.table {
  border-spacing: 0 15px;
}

i {
  font-size: 1rem !important;
}

.table tr {
  border-radius: 20px;
}

tr td:nth-child(n + 5),
tr th:nth-child(n + 5) {
  border-radius: 0 0.625rem 0.625rem 0;
}

tr td:nth-child(1),
tr th:nth-child(1) {
  border-radius: 0.625rem 0 0 0.625rem;
}
</style>