<template lang="pug">
b-card.card-product.mt-5(img-top :img-src='product.image')
  b-card-body
    b-card-title
      router-link(:to='"/product/" + product._id') {{ product.name }}
    b-card-sub-title {{ product.category }} - {{ 'NTD:' + product.price }}
    b-card-text(style="color: lightslategray;") {{ product.description }}
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true
    }
  }
}
</script>
