<template>
  <div>

    <b-modal id="editStockModal" title="Stock Entry" ok-title="Save Stock" @ok="onSubmit">
      <form action="#">
        <b-form-group
          label="Item Name"
          label-for="item_name"
        >
          <b-form-input id="item_name" v-model="stock.item_name" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Description"
          label-for="description"
        >
          <b-form-input id="description" v-model="stock.description" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Unit Price"
          label-for="price"
        >
          <b-form-input id="price" v-model="stock.price" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Quantity"
          label-for="quantity"
        >
          <b-form-input id="quantity" v-model="stock.quantity" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Category"
          label-for="category"
        >
          <b-form-select v-model="stock.category" :options="categories"></b-form-select>
        </b-form-group>

        <b-form-group
          label="Date Acquired"
          label-for="acquired_on"
        >
          <b-form-input id="acquired_on" type="date" v-model="stock.acquired_on" trim></b-form-input>
        </b-form-group>


      </form>
    </b-modal>
  </div>
</template>

<script>
export default {
   props: {
    stock: {}
  },
  data() {
    return {
      categories: [
        {value: 'elctronics', text: 'Electronics'},
        {value: 'food', text: 'Food/Beverages'},
        {value: 'toiletries', text: 'Toiletries'},
        {value: 'home', text: 'Home & Fashion'},
        {value: 'furniture', text: 'Furnitures'},
      ]
    }
  },
  methods: {
    async onSubmit() {
      this.$axios.put('/api/stocks/' + this.stock.id, this.stock)
      .then((res)=>{
        if(res.status==202) {
          alert('Update successful!')
        }
      })
      .catch((err)=>{
        alert(err.message)
      })
    }
  }
}
</script>
