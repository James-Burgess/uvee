<template>
  <div id="app">
    <transition>
      <weather-loader v-if="loading"/>
    </transition>
    <sun-icon v-if="uvResult" :uv-info="uvResult.result"/>
  </div>
</template>

<script>
import WeatherLoader from '@/components/loader'
import SunIcon from '@/components/sun'

export default {
  name: 'App',
  components: {
    WeatherLoader,
    SunIcon
  },
  data () {
    return {
      loading: true,
      uvResult: {},
    }
  },
  mounted() {
    this.loadUV()
  }, methods: {
    async loadUV() {
      const myHeaders = new Headers();
      myHeaders.append("x-access-token", "f213f2f4c299a9f56657218255cd5c2b");
      myHeaders.append("Content-Type", "application/json");

      const requestOptions = {
        method: 'GET',
        headers: myHeaders,
        redirect: 'follow'
      };

      await fetch("https://api.openuv.io/api/v1/uv?lat=-34.033332&lng=18.3499986&alt=0&dt=", requestOptions)
          .then(response => response.json())
          .then(result => this.uvResult = result)
          .catch(error => console.log('error', error));

      // this.loading = false

      window.setTimeout(() => {
        this.loading = false
      },
      500
      )

    }
  }
}
</script>

<style>
.v-enter-active,
.v-leave-active {
  transition: all 0.5s ease-out;
  transform: scale(2);
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
