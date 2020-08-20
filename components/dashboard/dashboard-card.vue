<template>
  <v-card class="mx-auto" max-width="344" outlined>
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">{{ title }}</div>
        <v-list-item-subtitle>{{ results }}</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>
  </v-card>
</template>

<script>
export default {
  props: {
    title: String,
    results: Number
  }
};
</script>

<style>
</style>
