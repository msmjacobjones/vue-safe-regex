<template>
  <div v-show="isUserLoggedIn">
  <panel title="RegChecker">
    <v-text-field
      label="Check your RegEx"
      v-model="newText"
    ></v-text-field>
  </panel>
  <v-btn
    dark
    class="cyan"
    @click="checkRegEx">
    Check
  </v-btn>


    <article :class="isSuccess" v-if="isShown">
      <div class="message-header" >
        <p>{{ regExMessageTitle + regExMessage }}</p>
        <button class="delete" aria-label="delete" @click="isShown = false"></button>
      </div>
    </article>
  </div>
</template>

<script>
  import {mapState} from 'vuex'
  import safe from 'safe-regex'
  export default {
    data () {
      return {
        newText: '',
        isSuccess: '',
        regExMessageTitle: '',
        regExMessage: '',
        isShown: false
      }
    },
    computed: {
      ...mapState([
        'isUserLoggedIn'
      ])
    },
    methods: {
      checkRegEx () {
        if (typeof this.newText !== 'string') return alert('Please Enter Correct RegEx')

        let regex
        regex = this.newText
        let ok = safe(regex)
        if (ok) {
          this.isSuccess = 'message is-success'
          this.isShown = true
          this.regExMessageTitle = 'Success '
          this.regExMessage = 'This RegEx is safe for use: ' + this.newText
        } else {
          this.isSuccess = 'message is-danger'
          this.isShown = true
          this.regExMessageTitle = 'WARNING!! '
          this.regExMessage = 'POTENTIAL RISK IF THIS REGEX IS IMPLEMENTED: ' + this.newText
        }
        this.newText = ''
      }
    }
  }
</script>

<style>

</style>
