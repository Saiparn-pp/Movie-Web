<template>
  <v-app light>
    <v-app-bar class="custom" clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon class="custom" @click.stop="fixed = !fixed" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? "right" : "left"}` }}</v-icon>
      </v-btn>

      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>

      <!-- <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>mdi-minus</v-icon>
      </v-btn> -->
      <v-toolbar-title>{{ title }}</v-toolbar-title>
      <v-spacer />

      <v-btn icon @click.stop="mdi - account">
        <v-icon>mdi-account</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main color="#d0f0c0">
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer class="custom" :absolute="!fixed" app>
      <span>
        <v-row>
          <v-col color="white">
            <h3 color="white">Genres :</h3>
          </v-col>
          <v-col color="white">
            <h4>Genres</h4>
            <h4>Genres</h4>
            <h4>Genres</h4>
          </v-col>
          <v-col color="white">
            <h4>Genres</h4>
            <h4>Genres</h4>
            <h4>Genres</h4>
          </v-col>
        </v-row>
      </span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-chart-bubble",
          title: "Inspire",
          to: "/inspire",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Movie Night",
    };
  },
};
</script>

<style>
.custom {
  background: linear-Gradient(to bottom right, #94b9ff, #cdffd8);
}
</style>
