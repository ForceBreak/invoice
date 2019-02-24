<template>
  <v-flex xs12 sm6 class="relative">
    <h6 class='title'>{{ name }}</h6>
     <v-menu
        v-model="showPicker"
        :close-on-content-click="false"
        :nudge-right="40"
        lazy
        transition="scale-transition"
        offset-y
        full-width
        bottom
        min-width="290px"
      >
        <v-text-field
          slot="activator"
          append-icon="event"
          :placeholder="nameChoice" 
          :value="date"
          :rules="textRule"
          required
        />
        <v-date-picker 
          v-model="date" 
          @input="showPicker = false"
        />
      </v-menu>
  </v-flex>
</template>

<script>
  export default {
    props: [
      'name',
      'textRule',
      'placeholder'
    ],
    data () {
      return {
        date: '',
        showPicker: false,
        months: [
          'January',
          'February',
          'March',
          'April',
          'May',
          'June',
          'July',
          'August',
          'September',
          'October',
          'November',
          'December'
        ]
      }
    },
    computed: {
      nameChoice () {
        if (this.placeholder) {
          return this.placeholder
        } else {
          return this.name
        }
      }
    },
    methods: {
      sendDate () {
        let arrDate = this.date.split('-')
        let month = this.months[Number(arrDate[1])]
        let formattedDate = `${arrDate[2]} ${month} ${arrDate[0]}`
        this.$emit('date', {
          date: formattedDate
        })
      }
    },
    watch: {
      showPicker: function () {
        if (this.showPicker === false) {
          this.sendDate()
        }
      }
    }
  }
</script>

<style scoped>
.relative{
  position: relative;
}
</style>