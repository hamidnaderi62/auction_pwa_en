<template>
  <v-bottom-navigation
    :value="value"
    color="primary"
    grow
  >
    <v-btn to="/auctionpage">
      <span> All Auctions</span>
      <v-icon>mdi-format-list-bulleted-square</v-icon>
    </v-btn>

    <v-btn to="/myauctionpage">
      <span> My Auctions</span>
      <v-icon>mdi-playlist-star</v-icon>
    </v-btn>

    <v-btn to="/auctioncreatepage">
      <span> New </span>
      <v-icon>mdi-pencil</v-icon>
    </v-btn>


  </v-bottom-navigation>
</template>

<script>
  export default {
    data: () => ({ value: 1 }),
  }
</script>