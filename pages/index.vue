<template>
  <v-layout wrap>
    <h2 class='display-3'>Invoices</h2>
    <v-flex xs12>
      <h6 class='title'>Actions</h6>
      <v-btn color='info' nuxt :to="'/create'">
        Add new
      </v-btn>
    </v-flex>
    <v-flex xs12>
      <h6 class='title'>Invoices</h6>
      <v-data-table
        :headers='headers'
        :items='invoices'
        class='elevation-1'
      >
        <template slot='items' slot-scope='props'>
          <td class='no_wrap'>{{ props.item.date_created }}</td>
          <td class='no_wrap'>{{ props.item.number }}</td>
          <td class='no_wrap'>{{ props.item.date_supply }}</td>
          <td>{{ props.item.comment }}</td>
          <td>
            <v-btn color='info' small nuxt :to="`${props.item.id}`">Edit</v-btn>
            <v-btn color='warning' small @click="remove(props.index)">Remove</v-btn>
          </td>
        </template>
      </v-data-table>
    </v-flex>
  </v-layout>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'
export default {
  data () {
    return {
      headers: [
        {
          text: 'Create',
          align: 'left',
          sortable: false,
          value: 'date_created'
        },
        { text: 'No', value: 'number', sortable: false },
        { text: 'Supply', value: 'date_supply', sortable: false },
        { text: 'Comment', value: 'comment', sortable: false },
        { text: 'Actions', value: 'actions', sortable: false }
      ]
    }
  },
  methods: {
    remove (item) {
      this.$store.commit('REMOVE_INVOICE', item)
    }
  },
  computed: {
    ...mapMutations({
      REMOVE_INVOICE: 'REMOVE_INVOICE'
    }),
    ...mapGetters({
      invoices: 'invoices'
    })
  }
}
</script>
<style scoped>
  .no_wrap{
    white-space: nowrap;
  }
</style>