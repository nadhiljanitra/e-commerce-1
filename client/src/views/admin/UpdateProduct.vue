<template>
  <div id="updatePage">
    <div id="uProductList">
      <simple-card v-for="product in products" :key="product.i" :product="product" @card="setCard"></simple-card>
    </div>
    <div id="uProductDetail">
      <div v-if="!empty">
        <update :prod="prod" @bukanupdate="kosongin"></update>

      </div>
      <div v-if="empty" id="emptyMessage">
        <h5>Select product from product list</h5>
      </div>

    </div>
  </div>
</template>

<script>
import SimpleCard from '@/components/CardSimple.vue'
import { mapState } from 'vuex'
import Update from '@/components/Update.vue'

export default {
  components : {
    SimpleCard,
    Update
  },
  data(){
    return {
      prod : {},
      empty : true
    }
  },
  methods: {
    getProduct(){
      if (this.products.length < 1){
        this.$store.dispatch('products/getProduct')
      }
    },
    setCard(card){
      this.empty = false
      this.prod = card
    },
    kosongin(){
      console.log('masuk kosongi');
      this.empty = true
    }
  },
  computed: {
    ...mapState('products',[
      'products'
    ])
  },
  created(){
    this.getProduct()
    this.$emit('bukanhome')
  }
}
</script>

<style>
#updatePage{
  display: flex;
  flex-direction: row
}
#uProductList{
  width: 25%;
  height: 100vh;
  overflow: scroll;
  padding: 10px 5px;
  overflow-x: hidden
}
#uProductDetail{
  width: 100%;
}
#emptyMessage{
  margin: 20px
}
</style>