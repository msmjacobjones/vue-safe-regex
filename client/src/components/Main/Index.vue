<template>
  <v-layout>
    <v-flex :class="{
        xs6: !isUserLoggedIn,
        xs6: isUserLoggedIn,
      }" class="text-xs-center">
      <reg-ex-search-panel class="text-xs-center" />
    </v-flex>
  </v-layout>
</template>

<script>
import RegExSearchPanel from './RegExSearchPanel'
import {mapState} from 'vuex'

export default {
  components: {
    RegExSearchPanel
  },
  computed: {
    ...mapState([
      'isUserLoggedIn'
    ])
  },
  data () {
    return {
      songs: null
    }
  }
}
</script>

