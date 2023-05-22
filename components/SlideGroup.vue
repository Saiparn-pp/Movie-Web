<template>
  <v-sheet class="mx-auto" elevation="8" max-width="800">
    <v-slide-group show-arrows>
      <v-slide-group-item v-for="data in filteredItems" :key="data.id">
        <v-img @click="handleItemClick(data)" :src="data.image.medium"></v-img>
      </v-slide-group-item>
    </v-slide-group>
  </v-sheet>
</template>

<script>
export default {
  name: "SlideGroup",
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  computed: {
    filteredItems() {
      return this.items.filter((item) => item.rating > 8);
    },
  },
  methods: {
    handleItemClick(data) {
      this.$emit("item-click", data);
    },
  },
};
</script>
