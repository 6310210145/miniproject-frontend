<template>
<div>
<v-data-table
    :headers="headers"
    :items="restaurantItem"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Restaurant</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-btn
              color="primary"
              dark
              class="mb-2"
              @click="openDialog('add', defaultItem)"
            >
              เพิ่มข้อมูล
            </v-btn>

      </v-toolbar>
    </template>
    <template v-slot:[`item.actions`] = "{ item }">
      <v-btn small outlined @click="openDialog('edit', item)" color="blue">
      <v-icon>
        mdi-pencil
      </v-icon>
      </v-btn>
      <v-btn small outlined @click="deleteItem(item)" color="red" class="ml-2">
      <v-icon>
        mdi-delete
      </v-icon>
      </v-btn>
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
  <v-dialog
          v-model="dialogCreate"
          max-width="500px"
        >
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                    <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="restaurantId"
                      label="รหัสร้านค้า"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="restaurantname"
                      label="ชื่อร้านค้า"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="restaurantdetail"
                      label="รายละเอียดร้านค้า"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                ยกเลิก
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save(formTitle)"
              >
                บันทึกข้อมูล
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5">ตุณต้องการลบข้อมูลนี้ในตารางใช่ หรือ ไม่?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">ยกเลิก</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">ตกลง</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
</div>
</template>

<script>
export default {
  data: () => ({
    restaurantId: '',
    restaurantname: '',
    restaurantdetail: '',
    dialogCreate: false,
    dialogDelete: false,
    headers: [
      {
        text: 'ไอดี',
        align: 'start',
        sortable: false,
        value: 'id'
      },
      { text: 'รหัสร้านค้า', value: 'restaurantId' },
      { text: 'ชื่อร้านค้า', value: 'restaurantname' },
      { text: 'รายละเอียดร้านค้า', value: 'restaurantdetail' },
      { text: 'จัดการ', value: 'actions', sortable: false }
    ],
    restaurantItem: [],
    editedIndex: -1,
    editedItem: {
      name: '',
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0
    },
    defaultItem: {
      name: '',
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0
    },
    formTitle: '',
    idRestaurant: '',
    idforDelete: ''
  }),

  watch: {
    dialog (val) {
      val || this.close()
    },
    dialogDelete (val) {
      val || this.closeDelete()
    }
  },

  created () {
    this.initialize()
  },

  methods: {
    async initialize () {
      this.restaurantItem = []
      try {
        var data = await this.axios.get('http://localhost:9000/restaurant')
        console.log('data restaurant ====>', data)
        this.restaurantItem = data.data
      } catch (error) {

      }
    },
    openDialog (Action, item) {
      this.formTitle = ''
      if (Action === 'add') {
        this.dialogCreate = true
        this.formTitle = 'เพิ่มข้อมูล'
        this.editedItem = item
      } else {
        this.formTitle = 'แก้ไขข้อมูล'
        this.dialogCreate = true
        this.restaurantId = item.restaurantId
        this.restaurantname = item.restaurantname
        this.restaurantdetail = item.restaurantdetail
        this.idRestaurant = item.id
      }
    },

    editItem (item) {
      console.log('item select', item)
      this.editedIndex = this.restaurantItem.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },

    deleteItem (item) {
      this.idforDelete = item.id
      this.dialogDelete = true
    },

    async deleteItemConfirm () {
      try {
        var response = await this.axios.delete('http://localhost:9000/restaurant/' + this.idforDelete)
        this.initialize()
      } catch (error) {
        console.log(error.message)
      }
      this.closeDelete()
    },

    close () {
      this.dialogCreate = false
      this.editedItem = []
      this.editedIndex = -1
      this.defaultItem = {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0
      }
    },

    closeDelete () {
      this.dialogDelete = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },

    async save (action) {
      var data = {
        restaurantId: this.restaurantId,
        restaurantname: this.restaurantname,
        restaurantdetail: this.restaurantdetail,
      }
      if (action === 'เพิ่มข้อมูล') {
        try {
          var dataResponse = await this.axios.post('http://localhost:9000/restaurant', data)
          console.log('dataResponse ====>', dataResponse)
          this.close()
          this.initialize()
        } catch (error) {
          console.log(error.message)
        }
      } else {
        try {
          var dataResponse = await this.axios.put('http://localhost:9000/restaurant/' + this.idRestaurant, data)
          console.log('dataResponse ====>', dataResponse)
          this.close()
          this.initialize()
        } catch (error) {
          console.log(error.message)
        }
      }
    }
  }
}
</script>

<style>

</style>