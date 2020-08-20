<template>
  <v-container class="grey lighten-5">
    <v-row>
      <v-col>
        <h1 class="index-title">
          COVID19 GLOBAL VIEWER APP
        </h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <div class="index-btn">
          <v-btn to="/dashboard" class="btn">
            Go to Dashboard
          </v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {};
</script>

<style>
.index-title,
.index-btn {
  align-items: center;
  justify-content: center;
  display: flex;
}
</style>
