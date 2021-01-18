<template>
  <v-app>
   <div>
     <v-app-bar
  color="blue"
></v-app-bar>
   </div>
    <v-main>
      <List/>
    </v-main>
  </v-app>
</template>

<script>
import List from './components/List'

export default {
  name: 'App',

  components: {
    List
  },

  data: () => ({
    //
  })
}
</script>
