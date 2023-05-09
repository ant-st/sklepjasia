<script>
export default {
  name: "StoreCreator",
  props: {
    categories: Array
  },
  data() {
    return {
      newCategory: '',
      newItem: {
        label: null,
        price: null,
        animalCategory: null,
        treeMounted: false,
      }
    }
  },
  methods: {
    submitNewItem() {
      if (this.newCategory) this.newItem.animalCategory = this.newCategory;
      this.$emit('created',this.newItem);
      this.newItem = {
        label: null,
        price: null,
        animalCategory: null,
        treeMounted: false,
      };
      this.newCategory = '';
    }
  }
}

</script>

<template>

  <div id="item-creator" >
    <h3>Dodaj nowy produkt:</h3>
    <form @submit.prevent="submitNewItem">
      <label>Nowy produkt: <input placeholder="Nazwa" required v-model="newItem.label"/>  </label>
      <label>Cena w zł: <input placeholder="Cena w zł" type="number" required v-model="newItem.price"/>  </label>
      <label>Kategoria:
        <select v-model="newItem.animalCategory" required>
          <option v-for="category in categories">{{category}}</option>
          <option>Inna</option>
        </select>
        <input placeholder = 'Nowa kategoria' v-if="newItem.animalCategory === 'Inna'" required v-model="newCategory"/>
      </label>
      <label>Montaż: <p>{{newItem.treeMounted ? '🌳 na drzewie' : '🏕️ na gruncie'}}</p><input type="checkbox" v-model="newItem.treeMounted" id="checkbox"></label>
      <button type="submit">Dodaj!</button>
    </form>
  </div>

</template>



<style scoped>

  #item-creator {
    margin: 30px 10px;
    border: 2px solid #B89100;
    border-radius: 10px;
    padding: 10px;
    box-sizing: border-box;
    background-color: rgba(184, 144, 0, 0.1);
    color: #ebebeb;
  }

  #item-creator h3 {
    padding-left: 20px;
  }

  #item-creator form {
    display: flex;
    flex-direction: column;
    width: 90%;
    margin: 10px auto;
  }

  #item-creator label {
    display: inline-flex;
    justify-content: space-between;
    margin: 10px;
  }

  #item-creator p {
    width: 50%;
    margin: 0;
  }

  #item-creator input, #item-creator select {
    width: 50%;
    background: none;
    border: none;
    border-bottom: 1px solid #B89100;
    color: #ebebeb;
  }

  input#checkbox {
    height: 20px;
    width: 20px;
  }

  #item-creator button {
    width: 60%;
    padding: 10px;
    margin: 0 auto;
    border-color: #B89100;
    transition: border 0.2s linear;
  }

  #item-creator button:hover {
    border-color: #ebebeb;
  }

</style>