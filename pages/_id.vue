<template>
  <div class="container">
    <v-row>
      <img justify="center" :src="datas[0].image.medium" height="400" />
      <v-col cols="5">
        <div>
          <h1>เรื่อง {{ datas[0].name }}</h1>
          <v-text v-for="genre in datas[0].genres" :key="genre.genres">
            {{ genre }},
          </v-text>
          <p>Runtime : {{ datas[0].runtime }} min</p>
          <p>Language : {{ datas[0].language }}</p>
          <p>Ended : {{ datas[0].ended }}</p>
          <p>premiered : {{ datas[0].premiered }}</p>
          <p>
            schedule :
            <v-text v-for="day in datas[0].schedule.days" :key="day.schedule">
              {{ day }}
            </v-text>
            at
            <v-text v-for="time in datas[0].schedule.time" :key="time.schedule">
              {{ time }}
            </v-text>
          </p>

          <p>status : {{ datas[0].status }}</p>

          <p>
            externals :
            <v-text
              v-for="external in datas[0].externals"
              :key="external.externals"
            >
              {{ external }}
            </v-text>
          </p>
        </div>
      </v-col>
      <v-col>
        <v-card
          class="d-flex flex-column mx-auto py-8"
          elevation="10"
          height="200"
          width="360"
        >
          <div class="d-flex justify-center mt-auto text-h5">
            Rating overview
          </div>

          <div class="d-flex align-center flex-column my-auto">
            <div class="text-h3 mt-5">
              <v-text>
                {{ datas[0].rating.average }}
              </v-text>
              <span class="text-h6 ml-n1"> /10</span>
            </div>

            <v-rating
              :value="Math.ceil(datas[0].rating.average) / 2"
              readonly
              color="yellow"
              half-increments
            ></v-rating>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    const { data } = await $axios.get("https://api.tvmaze.com/shows");
    console.log(data);
    const filteredData = data.filter((key) => key.id === Number(params.id));
    // this.datas = filteredData;
    return { datas: filteredData };
  },
};
</script>

<style></style>
