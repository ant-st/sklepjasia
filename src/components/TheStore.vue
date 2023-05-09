<script>
import StoreItem from "@/components/StoreItem.vue";
import StoreCreator from "@/components/StoreCreator.vue";
import StoreFilter from "@/components/StoreFilter.vue";
import TheLogger from "@/components/TheLogger.vue";
import TheCurrencySelector from "@/components/TheCurrencySelector.vue";
import {defaultStoreItems} from "@/seed";

export default {
  name: "TheStore",
  props: {
    loggedIn: Boolean
  },
  components: {TheCurrencySelector, TheLogger, StoreFilter, StoreCreator, StoreItem},
  data() {
    return {
      showFilters: false,
      storeItems: defaultStoreItems,
      filter: {
        animalCategory: '',
        treeMounted: 0,
        label: '',
        sort: 'id +'
      },
      loggedIn: false,
      currency: {
          "code": "PLN",
          "value": 1
        },
    }
  },
  methods: {
    addNewItem(item) {
      let newItem = {...item, id: this.storeItems[this.storeItems.length-1].id+1};
      this.storeItems.push(newItem);
    },
    handleDelete(itemId) {
      this.storeItems = this.storeItems.filter(el => el.id !== itemId)
    },
    handleFilterChange(filter) {
      this.filter = filter;
    },
    handleLogIn() {
      this.loggedIn = true;
    },
    handleLogOut() {
      this.loggedIn = false;
    },
    handleCurrencyChange(currency) {
      this.currency = currency;
    }
  },
  computed: {
    getCategories() {
      return [...new Set(this.storeItems.map(item => item.animalCategory))];
    },
    getFilteredStoreItems() {
      let filteredItems = this.storeItems.filter(element => {
        if (
            element.label.toLowerCase().includes(this.filter.label.toLowerCase())
            &&
            element.animalCategory.toLowerCase().includes(this.filter.animalCategory.toLowerCase())
            &&
            (!Number(this.filter.treeMounted) || (element.treeMounted && Number(this.filter.treeMounted) === 1) || (!element.treeMounted && Number(this.filter.treeMounted) === 2))
        ) return element;
      });

      const sortParams = this.filter.sort.split(' ');

      if (sortParams[1] === '+') {
        filteredItems.sort((a, b) => (a[sortParams[0]] > b[sortParams[0]]) ? 1 : -1)
      }
      else {
        filteredItems.sort((a, b) => (a[sortParams[0]] < b[sortParams[0]]) ? 1 : -1)
      }

      return filteredItems;
    }
  }
}
</script>

<template>
  <div id="settings" :class='{showFilters}'>
    <TheLogger
        :loggedIn = loggedIn
        @logout = handleLogOut
        @login = handleLogIn
    />
    <label class="mobile">Pokaż filtry: <input type="checkbox" v-model="showFilters"/></label>
    <div id="filters" :class="{showFilters}">
      <TheCurrencySelector
          @currency = "handleCurrencyChange"
      />
      <StoreFilter
          :categories = getCategories
          @filterChanged = 'handleFilterChange'
      />
      <StoreCreator
          v-if = "loggedIn"
          :categories = getCategories
          @created = 'addNewItem'
      />
      <label class="mobile">Pokaż filtry: <input type="checkbox" v-model="showFilters"/></label>
    </div>
  </div>
  <div id="the-store">
    <h2>Dostępne przedmioty:</h2>
    <div id="store-item-list">
      <StoreItem
          v-if = "getFilteredStoreItems.length"
          v-for="item in getFilteredStoreItems"
          :item="item"
          :key="item.id"
          :loggedIn="loggedIn"
          :currency="currency"
          @deleteItem = 'handleDelete'
      />
      <p v-else>Nie znaleziono przedmiotów dla wybranych filtrów :(</p>
    </div>
  </div>

</template>


<style scoped>

.mobile {
  display: none;
}

#the-store {
  grid-area: store;
  text-align: center;
  overflow: scroll;
}

#the-store h2 {
  color: #f8f8f8;
  margin: 30px auto;
}

#settings {
  grid-area: settings;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}


#store-item-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

@media screen and (max-width: 650px) {
  .mobile {
    display: inline;
  }
  #settings {
    height: 100px;
    overflow: hidden;
  }
  #filters {
    display: none;
  }
  #filters.showFilters {
    display: inline;
  }
  #settings.showFilters {
    height: auto;
  }
}
</style>