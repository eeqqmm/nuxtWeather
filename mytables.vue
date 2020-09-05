<template>
  <div>
    <v-layout>
      <v-flex colomn xs12>
        <v-for v-for="info in cityInfo" :key="info.id">
          <v-flex xs12 md7 class="mt-2">
            <v-card>
              <v-card-text>
                <v-flex row>
                  <v-flex v-if="info" column xs5 class="pa-1">
                    <h4>City</h4>
                    <h2 class="display-1">{{ info.name }}</h2>
                    <img
                      :src="`https://openweathermap.org/img/wn/${info.weather[0].icon}@2x.png`"
                      alt="weather icon"
                    />
                  </v-flex>
                  <v-flex column xs6 class="pa-1">
                    <h2 class="display-1">
                      {{ Math.round(info.main.temp - 273) }} C&deg;
                    </h2>
                    <span class="caption">
                      {{ info.weather[0].description }}</span
                    >
                    <h3 class="headline">
                      wind {{ info.wind.speed }} m/s ({{ info.wind.deg }}
                      &deg;)
                    </h3>
                    <h3 class="headline">
                      Humidity: {{ info.main.humidity }}%
                    </h3>
                    <h3 class="headline">
                      Pressure: {{ info.main.pressure }}hPa
                    </h3>
                  </v-flex>
                  <v-flex column xs1>
                    <v-btn icon color="red" @click="removeCity(n)">
                      <v-icon>mdi-close</v-icon>
                    </v-btn>
                  </v-flex>
                </v-flex>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-for>
      </v-flex>
    </v-layout>
    <v-flex xs12 md7 justify-space-between row class="mt-4">
      <v-btn @click="DeleteAll()">
        <span>Remove all</span>
      </v-btn>
      <v-btn>
        <nuxt-link to="/"> <span>Add city</span></nuxt-link>
      </v-btn>
    </v-flex>
  </div>
</template>

<script>
export default {
  name: 'Tables',
  data: () => ({
    cities: [],
    cityInfo: [],
    weather: '',
  }),
  // computed: {
  //   icon() {
  //     return this.cityInfo[index].weather
  //       ? `https://openweathermap.org/img/wn/${this.cityInfo.weather[0].icon}@2x.png`
  //       : ''
  //   },
  // },
  mounted() {
    if (localStorage.getItem('cities')) {
      try {
        this.cities = JSON.parse(localStorage.getItem('cities'))
      } catch (e) {
        localStorage.removeItem('cities')
      }
    }
    this.cities.forEach((element) => {
      this.$axios
        .$get(
          `https://api.openweathermap.org/data/2.5/weather?q=${element}&appid=279b9f63c329a284f11f36e27f0eb4bb`
        )
        .then((res) => this.cityInfo.push((this.weather = res)))
    })
    console.log(this.citiInfo)
  },
  methods: {
    saveCity() {
      const parsed = JSON.stringify(this.cities)
      localStorage.setItem('cities', parsed)
    },
    removeCity(x) {
      this.cities.splice(x, 1)
      this.cityInfo.splice(x, 1)
      this.saveCity()
    },
    DeleteAll() {
      localStorage.clear()
      this.cityInfo.splice(0)
      this.cities.splice(0)
    },
  },
}
</script>
