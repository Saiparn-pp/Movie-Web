<template>
  <div class="container">
    <div>
      <v-row>
        <v-col>
          <v-text-field
            style="max-width: 300px"
            prepend-icon="mdi-magnify"
            label="Search"
            v-model="searchQuery"
            single-line
          ></v-text-field>
        </v-col>
        <v-col align="right">
          <v-select
            style="max-width: 400px"
            v-model="value"
            :items="items"
            label="Genres"
            multiple
            chips
          ></v-select>
        </v-col>
      </v-row>
    </div>
    <v-row>
      <v-col
        v-for="data in filteredData"
        :key="data.id"
        align="center"
        justify="center"
      >
        <v-hover>
          <v-card
            class="mx-auto hover-shadow"
            height="520"
            max-width="350"
            @click="changeRoute(data)"
          >
            <v-card-text
              class="font-weight-medium mt-12 text-center text-subtitle-1"
            >
              <v-img :src="data.image.medium">
                <div class="py-1" align="right">
                  <v-card
                    color="#FEFF99"
                    height="25"
                    width="50"
                    v-if="data.rating"
                  >
                    <v-text align="center">
                      <p v-for="rating in data.rating">★{{ rating }}</p>
                    </v-text>
                  </v-card>
                </div>
              </v-img>

              <v-col
                block
                color="#121212"
                size="x-large"
                @click="changeRoute(data)"
              >
                <h2>{{ data.name }}</h2>
              </v-col>
              <v-chip
                class="ma-1"
                text-color="white"
                color="bar"
                size="x-small"
                v-for="genre in data.genres"
                :key="genre"
              >
                {{ genre }}
              </v-chip>
            </v-card-text>
          </v-card>
        </v-hover>
      </v-col>
    </v-row>
    <div class="container">
      <v-pagination
        v-model="currentPage"
        :length="Math.ceil(filteredData / perPage)"
        rounded="circle"
        @input="changePage"
      ></v-pagination>
    </div>
    <v-sheet class="mx-auto" elevation="8" max-width="800">
      <v-slide-group show-arrows>
        <v-slide-group-item v-for="data in this.datas" :key="data.id">
          <v-img @click="changeRoute(data)" :src="data.image.medium"></v-img>
        </v-slide-group-item>
      </v-slide-group>
    </v-sheet>
  </div>
</template>

<script>
export default {
  name: "InspirePage",
  methods: {
    changeRoute(data) {
      this.$router.push(`/${data.id}`);
    },
    changePage(page) {
      this.currentPage = page;
      this.fetchData();
    },
    async fetchData() {
      const currentPage = this.currentPage;
      const perPage = this.perPage;
      const startIndex = (currentPage - 1) * perPage;
      const endIndex = startIndex + perPage;

      try {
        const { data } = await this.$axios.get("https://api.tvmaze.com/shows");
        const paginatedData = data.slice(startIndex, endIndex);

        this.datas = paginatedData;
      } catch (error) {
        console.error(error);
      }
    },
  },

  data() {
    return {
      page: 1,
      perPage: 32,
      currentPage: 1,
      datas: [],
      searchQuery: "",
      items: ["Action", "Adventure", "Anime", "buzz"],
      value: ["foo", "Crime", "fizz", "buzz"],
    };
  },
  mounted() {
    this.fetchData();
  },
  computed: {
    filteredData() {
      return this.datas.filter((item) =>
        item.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
};
</script>

<style scoped>
/* .v-card.on-hover.v-theme--dark {
  background-color: rgba(#fff, 0.8);
}
.v-card__text {
  color: #000;
} */
/* @import "@/components/hover.css"; */
.hover-shadow {
  transition: box-shadow 0.3s;
}

.hover-shadow:hover {
  box-shadow: 0px 4px 10px 10px rgba(11, 81, 50, 0.2);
}
</style>
