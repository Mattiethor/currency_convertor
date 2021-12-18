<template>
  <div id="app">
    <div class="container-fluid">
      <div class="row">
        <div class="col-12">
          <Conversion :bankList="bankList" :amount="userAmount" />
        </div>
      </div>
      <hr />
      <div class="row user-amount-row">
        <!-- selecteble database. as of 18.12.2021 IB is broken -->
        <div class="col-2 button-group">
          <div>
            <button
              type="button"
              class="btn btn-secondary"
              @click="selectDatabase('https://apis.is/currency/m5')"
            >
              M5
            </button>
            <button
              type="button"
              class="btn btn-secondary"
              @click="selectDatabase('https://apis.is/currency/arion')"
            >
              Arion
            </button>
            <button
              type="button"
              class="btn btn-secondary"
              @click="selectDatabase('https://apis.is/currency/lb')"
            >
              LB
            </button>
          </div>
        </div>

        <div class="col m-2">
          <input
            v-model="userAmount"
            type="number"
            name="userAmount"
            placeholder="Enter Amount"
            class="form-control form-control-lg"
          />
        </div>
        <div class="col-2"></div>
      </div>
    </div>
  </div>
</template>

<script>
const axios = require("axios");

import Conversion from "./components/Conversion.vue";

export default {
  name: "App",
  components: {
    Conversion,
  },
  data: () => {
    return {
      bankList: [],
      userAmount: 0,
      url: "https://apis.is/currency/m5",
    };
  },
  methods: {
    selectDatabase(api) {
      this.url = api;
      console.log(api);
      axios
        .get(this.url)
        .then((results) => {
          this.bankList = results.data.results;
        })
        .catch((error) => console.log(error));
    },
  },

  mounted() {
    axios
      .get(this.url)
      .then((results) => {
        this.bankList = results.data.results;
      })
      .catch((error) => console.log(error));
  },
};
</script>

<style>
button {
  margin: 5px;
  width: 65px;
  height: 50px;
  text-align: center;
}
.button-group {
  margin-left: 32px;
}
</style>
