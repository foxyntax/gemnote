<template>
  <div id="dashboard">
    <h1>Welcome to Gemnote, {{ $store.state.user.firstName }}! </h1>
    <article>
      <!-- First Row -->
      <div class="row">
        <div id="orders">
          <div>
            <h3 class="card-title">Total number of orders this month</h3>
            <p class="card-data">{{ $store.state.data.totalOrders | toFormattedInt }}</p>
          </div>

          <div>
            <h3 class="card-title">Average number of shipments/month</h3>
            <div class="flex justify-between">
              <p class="card-data">{{ $store.state.data.averageShipments | toFormattedInt }}</p>
              <button>View Order</button>
            </div>
          </div>
        </div>

        <div id="inventory">
          <div>
            <div id="donut-chart">
              <apexchart
                :width="donut.width"
                height="auto"
                type="donut"
                :options="donut.options"
                :series="donut.series"
              ></apexchart>
            </div>
            <div class="flex-grow">
              <h3 class="card-title">Current Inventory</h3>
              <div class="flex justify-between">
                <p class="card-data">{{ $store.state.data.inventory | toFormattedInt }}</p>
                <button>Mangage inventory</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Second Row -->
      <div id="trends">
        <div class="card px-2 md:px-5">
          <div class="flex flex-row justify-between px-2 md:px-0">
            <h3 class="card-title">Trending gifts in your store</h3>

            <div class="card-head-btn">
              <button class="py-2 px-4">Send a gift</button>
            </div>
          </div>

          <Gallery showMoreUrl="#" :hiddenItems="3" :data="$store.state.data.trendingGifts" />

          <div class="mobile-actions">
            <button class="py-2 px-4">Send a gift</button>
          </div>
        </div>
      </div>
      <!-- Last Row -->
      <div id="reports">
        <div class="card px-1 md:px-5">
          <div class="flex flex-row justify-between px-2 md:px-0">
            <h3 class="card-title">Total gifts sent this year</h3>

            <div class="card-head-btn">
              <button class="py-2 px-4">Download report</button>
            </div>
          </div>

          <div class="w-full">
            <apexchart
                width="100%"
                height="300px"
                type="bar"
                :options="column.options"
                :series="column.series"
              ></apexchart>
          </div>

          <div class="mobile-actions">
            <button class="py-2 px-4">Download report</button>
          </div>
        </div>
      </div>
    </article>
  </div>
</template>

<script>
import filters from '@/mixins/filters'
import gallery from '@/components/gallery.vue'
export default {
  components: { gallery },
  mixins: [filters],
  data: () => ({
    donut: {
      width: (window.innerWidth >= 768) ? '160px' : '200px',
      series: [44, 56],
      options: {
        colors: ['#24292c', '#ededed'],
        labels: ['Investory', 'Free Space'],
        legend: {
          show: false
        },
        dataLabels: {
          enabled: false
        },
        plotOptions: {
          pie: {
            donut: {
              size: '75%'
            }
          }
        }
      }
    },
    column: {
      series: [{
        name: 'Monthly report',
        data: [150, 159, 120, 90, 170, 164, 100, 50, 94, 35, 140, 167]
      }],
      options: {
        colors: ['gray'],
        dataLabels: {
          enabled: false
        },
        legend: {
          show: false
        },
        xaxis: {
          categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'June', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
          labels: {
            style: {
              fontSize: '12px'
            }
          }
        }
      }
    }
  }),
  head: () => ({
    title: 'Gemnote | Dashboard',
    meta: [
      // SEO
      { hid: 'description', name: 'description', content: 'Gemnote VueJS Frontend Assessment' },
      { hid: 'keywords', name: 'keywords', content: 'Gemnote, swag and gifts, gifts, gift inventory' },
      { name: 'robots', content: 'noindex, nofollow' },
      // Social Media
      { property: 'og:site_name', content: 'Gemnote' },
      { property: 'og:title', content: 'Gemnote VueJS Frontend Assessment' },
      { property: 'og:description', content: 'Gemnote by VueJs | NuxtJS' },
      { property: 'og:image', content: 'https://assets.website-files.com/5c7449f43783556baa54bd0e/60540cde101f8399aa9f3a8d_Gemnote_WebCover.png' },
      { property: 'og:url', content: 'https://gemnote.com' },
      { property: 'og:url', content: 'https://gemnote.com' },
      { name: 'twitter:card', content: 'twitterCard' },
      { name: 'twitter:image:alt', content: 'Alt text for image' },
      { name: 'twitter:site', content: '@website-username' },
      { name: 'fb:app_id', content: 'your_app_id' }
    ]
  })
}
</script>

<style lang="scss">

</style>
