<script>
export default {
  name: "StoreFilter",
  emits: ['filterChanged'],
  props: {
    categories: Array
  },
  data() {
    return {
      filter: {
        animalCategory: '',
        treeMounted: 0,
        label: '',
        sort: 'id +'
      }
    }
  },
  watch:
      {
        filter: {
          handler(newVal, oldVal) {
            this.$emit('filterChanged', this.filter);
          },
          deep: true
        }
      },
}
</script>

<template>
  <div id="store-filter">
    <h3>Filtruj:</h3>
    <label>
      <p>Kategorie:</p>
      <select v-model = 'filter.animalCategory'>
        <option value="">Wszystkie</option>
        <option v-for="category in categories">{{category}}</option>
      </select>
    </label>
    <label>
      <p>Montaż:</p>
      <select v-model = filter.treeMounted>
        <option value=0>Wszystko</option>
        <option value=1>🌳 na drzewie</option>
        <option value=2>🏕️ na gruncie</option>
      </select>
    </label>
    <label>
      <p>Nazwa:</p>
      <input v-model = "filter.label" placeholder="Filtruj wg nazwy"/>
    </label>
    <label>
      <p>Sortowanie:</p>
      <select v-model = 'filter.sort'>
        <option value='id +'>ID rosnąco</option>
        <option value='id -'>ID malejąco</option>
        <option value='price +'>Cena rosnąco</option>
        <option value='price -'>Cena malejąco</option>
        <option value='label +'>Nazwa rosnąco</option>
        <option value='label -'>Nazwa malejąco</option>
      </select>
    </label>
  </div>
</template>



<style scoped>

#store-filter {
  display: flex;
  flex-direction: column;
  width: 90%;
  margin: 30px auto;

  background-color: rgba(184, 144, 0, 0.1);
  color: #ebebeb;

  border: 2px solid #B89100;
  border-radius: 10px;
  padding: 10px;
  box-sizing: border-box;
}

#store-filter label {
  display: inline-flex;
  justify-content: space-between;
  margin: 10px;
}

#store-filter p {
  width: 50%;
  margin: 0;
}

#store-filter input, #store-filter select {
  width: 50%;
  background: none;
  border: none;
  border-bottom: 1px solid #B89100;
  color: #ebebeb;
}

</style>