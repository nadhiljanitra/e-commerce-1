<template>
  <div id="contentHolder">
    <card v-for="product in filteredProducts" :key="product.i" :product="product"></card>
  </div>
</template>

<script>
import Card from '@/components/Card.vue'
import { mapState } from 'vuex'


export default {
  props: ['query'],
  components : {
    Card
  },
  methods: {
    getProduct(){
      this.$q.loading.show()
      this.$store.dispatch('products/getProduct')
        .then(()=>{
          this.$q.loading.hide()
        })
        .catch(()=>{
          this.$q.loading.hide()
        })
    }
  },
  computed: {
    ...mapState('products',[
      'products'
    ]),
    filteredProducts(){
        let find = this.query
          return this.products.filter((product)=>{
            let regex = new RegExp(find,'i')
            return product.name.match(regex)
          })
      }
  },
  created(){
    this.getProduct()
  }
}
</script>

<style scoped>
#contentHolder{
  width: 90%;
  margin: 6px auto;
  border-radius: 10px;
  padding: 2px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around
}
</style>