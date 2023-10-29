<template>
 <v-container>
    <v-row>
        <v-col cols="12">
         <Restaurant/>
        </v-col>
    </v-row>
 </v-container>
</template>

<script>
export default {
  components: {
    Restaurant: () => import('../components/Restaurant.vue')
  }
}
</script>

<style>

</style>