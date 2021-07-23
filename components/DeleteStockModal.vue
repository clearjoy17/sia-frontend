<template>
  <div>

    <b-modal id="deleteStockModal" title="Stock Entry" ok-title="Delete Stock" @ok="onDelete" ok-variant="danger">
      Are you sure about deleting this stock? <br>
      {{ stock.item_name }} {{ stock.description }}
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    stock: {}
  },
  methods: {
    async onDelete() {
      this.$axios.delete('/api/stocks/' + this.stock.id)
      .then((res)=>{
        if(res.status==202) {
          alert('Stock is deleted successfully!')
          this.$emit('onDeleted')
        }
      })
    }
  }
}
</script>
