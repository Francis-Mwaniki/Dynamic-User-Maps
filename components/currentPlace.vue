<template>
  <div>
    <div class="flex flex-col">
      <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
          <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
            <table class="min-w-full divide-y divide-gray-200">
              <thead class="bg-gray-800">
                <tr>
                  <th
                    scope="col"
                    class="px-6 py-3 text-left text-xs font-medium text-gray-200 uppercase tracking-wider"
                  >
                    Key
                  </th>
                  <th
                    scope="col"
                    class="px-6 py-3 text-left text-xs font-medium text-gray-200 uppercase tracking-wider"
                  >
                    Place
                  </th>
                </tr>
              </thead>
              <tbody class="bg-slate-800 divide-y divide-gray-700" v-for="loc in locs">
                <tr>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-100"
                  >
                    Location
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-200">
                    {{ loc.location }}
                  </td>
                </tr>
                <tr>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-100"
                  >
                    City
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-200">
                    {{ loc.city }}
                  </td>
                </tr>
                <tr>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-100"
                  >
                    Latitude
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-200">
                    {{ loc.latitude }}
                  </td>
                </tr>
                <tr>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-100"
                  >
                    Longitude
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-200">
                    {{ loc.longitude }}
                  </td>
                </tr>
                <tr>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-100"
                  >
                    Accuracy
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-200">
                    {{ loc.accuracy }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["load", "locs"],
};
</script>

<style scoped></style>
