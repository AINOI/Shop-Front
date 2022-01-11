<template lang="pug">
b-container#product
  b-overlay(:show='!sell')
    template(#overlay)
      h1.text-danger(style="font-weight: bolder; filter:drop-shadow(2px 2px 5px rgba(150,150,150,0.5))") 商品已下架 O w < キラッー☆
    b-row
      b-col(cols='6')
        h1 {{ name }}
      b-col(cols='6')
        h4.text-right ${{ price }}
        b-form-input(type='number' v-model.number='quantity' :state='quantityState' min='0')
        b-btn(variant='primary' @click='addCart') 加入購物車
      b-col(cols='12' style="display: flex; justify-content: center;")
        img.w-50.my-5(:src='image')
      b-col(cols='12')
        p.bg-dark.rounded.text-center.text-white(style='white-space: pre; fontSize:40px;') {{ description }}
</template>

<script>
export default {
  data () {
    return {
      name: '',
      price: 0,
      description: '',
      image: '',
      sell: false,
      category: '',
      quantity: 0
    }
  },
  methods: {
    addCart () {
      this.$store.dispatch('user/addCart', { product: this.$route.params.id, quantity: this.quantity })
    }
  },
  computed: {
    quantityState () {
      return this.quantity === 0 ? null : this.quantity > 0
    }
  },
  async created () {
    try {
      const { data } = await this.api.get('/products/' + this.$route.params.id)
      this.name = data.result.name
      this.price = data.result.price
      this.description = data.result.description
      this.image = data.result.image
      this.sell = data.result.sell
      this.category = data.result.category
      document.title = `購物網 | ${this.name}`
    } catch (error) {
      this.$router.push('/')
    }
  }
}
</script>
