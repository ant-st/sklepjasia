<script>
import {currencyURL} from "@/passwords";
export default {
  name: "TheCurrencySelector",
  emits: ['currency'],
  data() {
    return {
      selectedCurrency: 'PLN',
      currencyRatio: {
        "PLN": {
          "code": "PLN",
          "value": 1
        }
      }
    }
  },
  created() {
    fetch(currencyURL)
        .then(r => r.json())
        .then(r =>
            this.currencyRatio = {...this.currencyRatio, ...r.data}
        );
  },
  watch: {
    selectedCurrency(newVal, oldVal) {
      if (newVal !== oldVal) this.$emit('currency', this.currencyRatio[this.selectedCurrency])
    }
  }
}
</script>

<template>

  <div id="currency-selector">
    <label>
      <p>Waluta:</p>
      <select v-model="selectedCurrency">
        <option>PLN</option>
        <option>USD</option>
        <option>EUR</option>
        <option>GBP</option>
      </select>
    </label>
  </div>

</template>

<style scoped>

#currency-selector {
  width: 90%;
  margin: 70px auto 10px;

  border: 2px solid #B89100;
  border-radius: 10px;
  padding: 10px;
  box-sizing: border-box;

  background-color: rgba(184, 144, 0, 0.1);
  color: #ebebeb;
}

#currency-selector label {
  display: inline-flex;
  justify-content: space-between;
  width: 100%;
  padding: 10px;
}

#currency-selector p {
  width: 50%;
  margin: 0;
}

#currency-selector select {
  width: 50%;
  background: none;
  border: none;
  border-bottom: 1px solid #B89100;
  color: #ebebeb;
}

</style>