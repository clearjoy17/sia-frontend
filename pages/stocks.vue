<template>

  <div>
    <NavBar />
    <EditStockModal :stock="selectedStock" />
    <DeleteStockModal :stock="selectedStock" @onDeleted="getAll" />
    <div class="container">
      <h1>
        Stocks
        <stockEntryModal class="float-right" @onAdd="getAll" />
      </h1>
      <table class="table table-bordered tabled-striped">
        <thead>
          <tr class="bg-info text-white">
            <th>Item Name</th>
            <th>Description</th>
            <th>Unit Price</th>
            <th>Quantity</th>
            <th>Category</th>
            <th>&nbsp;</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="stock in stocks" :key="stock.id">
            <td>{{stock.item_name}}</td>
            <td>{{stock.description}}</td>
            <td>{{stock.price}}</td>
            <td>{{stock.quantity}}</td>
            <td>{{stock.category}}</td>
            <td>
              <b-button @click="onEdit(stock)" variant="info" size="sm">
                Edit
              </b-button>
              <b-button @click="onDelete(stock)" variant="danger" size="sm">
                Delete
              </b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>

</template>

<script>
export default {
  data() {
    return {
      stocks: [],
      selectedStock: {}
    }
  },
  methods: {
    async getAll() {
      await this.$axios.get('/api/stocks')
      .then((res)=>{
        if(res.status==200){
          this.stocks = res.data
        }
      })
    },
    onEdit(selectedStock) {
      this.selectedStock = selectedStock
      this.$bvModal.show('editStockModal')
    },
    onDelete(selectedStock) {
      this.selectedStock = selectedStock
      this.$bvModal.show('deleteStockModal')
    }
  },
  created() {
    this.getAll()
  }
}

</script>

<style>

</style>
