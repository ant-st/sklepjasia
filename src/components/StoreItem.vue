<script>
export default {
  name: "StoreItem",
  emits: ['deleteItem'],
  props: {item: Object, loggedIn: Boolean, currency: Object},
  methods: {
    deleteItem() {
      this.$emit('deleteItem', this.item.id)
    },
    getPrice(price) {
      let result = (price*this.currency.value).toFixed(2);
      switch (this.currency.code) {
        default:
          return result+' zł';
        case 'EUR':
          return result+'€';
        case 'USD':
          return '$'+result;
        case 'GBP':
          return '£'+result;
      }
    }
  }
}
</script>

<template>
  <div class="item">
    <div class="itemLabel">
      <h3>{{item.label}}: {{getPrice(item.price)}}</h3>
      <button v-if=loggedIn @click = 'deleteItem'>Usuń</button>
    </div>
    <h4>{{item.animalCategory}} - {{item.treeMounted ? '🌳' : '🏕️'}}</h4>
  </div>
</template>

<style scoped>
  .item {
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    width: 70%;

    border-radius: 10px;
    border: 2px solid #407700;
    text-align: center;
    margin: 10px;
    overflow: hidden;
  }

  .itemLabel {
    display: inline-flex;
    justify-content: space-between;
  }

  .item h3 {
    padding: 10px;
  }

  .item h4 {
    background-color: #407700;
    color: #ebebeb;
  }

  .item button {
    height: 30px;
    margin: auto 5px;
  }


</style>