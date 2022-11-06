<template>
    <v-layout justify-center align-center>
      <v-container fill-height>

        <v-row align="center" no-gutters>

          <v-col cols="12">
              <v-alert color="deep-orange" icon="mdi-fire" title="Instructions" variant="outlined">
                Nullam tincidunt adipiscing enim. In consectetuer turpis ut velit. Maecenas egestas arcu quis ligula mattis placerat. Praesent metus tellus, elementum eu, semper a, adipiscing nec, purus.
              </v-alert>
          </v-col>
        
        </v-row>

        <v-row justify="space-around" style="margin-top:10px">
          <v-col cols="12" md="8">
            <v-text-field label="Word" hide-details="auto" />
          </v-col>
          <v-col cols="12" md="4">
            <v-btn color="error" dark plain outlined class="mb-2" >
              New Production
            </v-btn>
          </v-col>
        </v-row>

      </v-container>
    </v-layout>
  </template>

  <!-------------------->

  <script>
  export default {
    data: () => ({
      dialog: false,
      dialogDelete: false,
      headers: [
        { text: 'Producer', align: 'center', sortable: false, value: 'producer'},
        { text: 'Products', align: 'center', sortable: false, value: 'products'},
      ],
      grammar: [],
      editedIndex: -1,
      editedItem: { producer: '', products: [] },
      defaultItem: { producer: '', products: [] },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () { this.grammar = []},

      editItem (item) {
        this.editedIndex = this.grammar.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        this.editedIndex = this.grammar.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

      deleteItemConfirm () {
        this.grammar.splice(this.editedIndex, 1)
        this.closeDelete()
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.grammar[this.editedIndex], this.editedItem)
        } else {
          this.grammar.push(this.editedItem)
        }
        this.close()
      },
    },
  }
</script>