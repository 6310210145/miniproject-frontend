<template>
  <v-container class="ma-5">
    <v-row>
      <v-col
        v-for="(restaurant, index) in restaurants"
        :key="index"
        cols="12"
        sm="6"
        md="4"
      >
        <v-card>
          <!-- Restaurant Image -->
          <v-carousel class="max-height-carousel">
            <v-carousel-item 
              v-for="(res,i) in restaurants"
              :key="i"
              :src="res.imageUrl"
              reverse-transition="fade-transition"
              transition="fade-transition"
              max-height="350px"
            ></v-carousel-item>
          </v-carousel>
          <v-card-title class="headline">
            {{ restaurant.name }}
          </v-card-title>
          <v-card-text>
            {{ restaurant.description }}
          </v-card-text>

          <v-card-actions >
            

            <v-btn color="amber" href="/res" >เลือกร้านอาหาร</v-btn>
            
          </v-card-actions>

        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      restaurants: [
        {
          name: "KFC",
          imageUrl: "https://images.unsplash.com/photo-1502998070258-dc1338445ac2?auto=format&fit=crop&q=80&w=1958&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          description: "Description for Restaurant 1",
        },
        {
          name: "shabu",
          imageUrl: "https://images.unsplash.com/photo-1502301103665-0b95cc738daf?auto=format&fit=crop&q=80&w=1964&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          description: "Description for Restaurant 2",
        },
        {
          name: "shabu 2",
          imageUrl: "https://images.unsplash.com/photo-1484980972926-edee96e0960d?auto=format&fit=crop&q=80&w=1974&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          description: "Description for Restaurant 3",
        },
        {
          name: "Omakase",
          imageUrl: "https://images.unsplash.com/photo-1484980972926-edee96e0960d?auto=format&fit=crop&q=80&w=1974&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          description: "Description for Restaurant 3",
        },
        {
          name: "Omakase 2",
          imageUrl: "https://images.unsplash.com/photo-1484980972926-edee96e0960d?auto=format&fit=crop&q=80&w=1974&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          description: "Description for Restaurant 3",
        },

        {
          name: "Omakase 3",
          imageUrl: "https://images.unsplash.com/photo-1484980972926-edee96e0960d?auto=format&fit=crop&q=80&w=1974&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          description: "Description for Restaurant 3",
        },
        // Add more restaurants as needed
      ],
    };
  },
};
</script>

<style>



.max-height-carousel {
  max-height: 350px; /* Adjust the max-height as needed */
}

</style>
