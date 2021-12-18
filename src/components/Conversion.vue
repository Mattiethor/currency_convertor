<template>
  <!-- converts the user typed number from ISK to the selected currency -->
  <div>
    <div class="row">
      <div class="col topBar border-bottom border-secondary">
        <h2>Currency Converter</h2>
      </div>
    </div>
    <div class="row">
      <div class="col-2">
      <div class="list-group currency-selector ">
        <ul>
          <li
            class="list-group-item list-group-item-action"
            @click="selectCurrency(currency)"
            v-for="(currency, index) in bankList"
            :key="index"
          >
            {{ currency.shortName }}
          </li>
        </ul>
        </div>
      </div>
      <div class="col">
        <div class="con-container">
          <div v-if="value">
            <h2>
               {{ convert }} ISK
            </h2>
          </div>
          <div v-else><h4>Select a currency</h4></div>
          
          <!-- display full name and conversion rate -->
          <CurrencyInfo
            :currency="selectedCurrency.longName"
            :rate="selectedCurrency.value"
          />
        </div>
      </div>
    </div>

    <!--<button @click="convert">Breyta</button>  -->
  </div>
</template>

<script>
import CurrencyInfo from "./Currency/CurrencyInfo.vue";

export default {
  name: "Conversion",
  props: ["bankList", "amount", "conversionRate"],
  components: {
    CurrencyInfo,
  },

  data: () => {
    return {
      value: undefined,
      convertedNumber: 0,
      selectedCurrency: [],
      shortName: undefined,
    };
  },

  methods: {
    selectCurrency(number) {
      this.selectedCurrency = number;
      this.value = number.value;
      console.log(this.selectedCurrency);
    },
  },
  computed: {
    convert() {
      let total = 0;
      total = this.amount * this.value;
      console.log(total);
      return total.toFixed(2);
    },
  },
};
</script>

<style>
.topBar {
  background-color: turquoise;
  color: white;
  height: 60px;
}

.con-container {
  text-align: center;
  margin-top: 200px;
}
li{
  margin: 5px;
  min-width: 30px;
  
}
.list-group-item{
  min-width: 60px;
  
}
</style>