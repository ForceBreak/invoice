<template>
  <v-layout>
    <v-form v-model="valid" class="flex xs12">
      <v-layout wrap>
        <v-flex xs12 sm6>
          <h6 class='title'>Number</h6>
          <v-text-field 
            :placeholder="'Invoice number'"
            append-icon="settings"
            v-model="number"
            :rules='textRule'
            required
          />
        </v-flex>
        <date-picker :name="'Invoice Date'" @date="invoiceDate" :textRule="textRule"/>
        <date-picker :name="'Supply Date'" @date="supplyDate" :textRule="textRule"/>
        <v-flex xs12>
          <h6 class='title'>Comment</h6>
          <v-textarea 
            :placeholder="'Comment'"
            v-model="comment"
            :rules='textRule'
            required
          />
        </v-flex>
        <v-flex xs12>
          <v-btn 
            color='success'
            @click="add_invoice"
            :disabled='!valid'
          >
            Save
          </v-btn>
          <v-btn 
            color='info'
            nuxt
            :to="'/'"
          >
            Home
          </v-btn>
      </v-flex>
      </v-layout>
    </v-form>
  </v-layout>
</template>

<script>
import datePicker from '@/components/datePicker'
import { mapMutations } from 'vuex'
export default {
  components: {
    datePicker
  },
  data () {
    return {
      valid: false,
      textRule: [
        v => !!v || 'Поле обязательно'
      ],
      comment: '',
      number: '',
      iDate: '',
      sDate: ''
    }
  },
  methods: {
    add_invoice () {
      this.$store.commit('ADD_INVOICE', {
        id: Date.now().toString(),
        number: this.number,
        date_created: this.iDate,
        date_supply: this.sDate,
        comment: this.comment
      })
    },
    invoiceDate (date) {
      this.iDate = date.date
    },
    supplyDate (date) {
      this.sDate = date.date
    }
  },
  computed: {
    ...mapMutations({
      ADD_INVOICE: 'ADD_INVOICE'
    })
  }
}
</script>

<style scoped>

</style>