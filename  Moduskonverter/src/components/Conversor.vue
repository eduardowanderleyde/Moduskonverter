<template>
  <div class="conversor">
    <h2>{{ moedaA }} zu {{ moedaB }}</h2>
    <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
    <input type="button" value="Moduskonverter" v-on:click="converter">
    <h2>{{ moedaB_value }}</h2>
  </div>
</template>

<script>
export default {
  name: 'ConversorUS',
  props: ['moedaA', 'moedaB'],
  data() {
    return {
      moedaA_value: "",
      moedaB_value: 0
    }
  },
  methods: {

    converter() {
      let de_para = this.moedaA + "_" + this.moedaB;
      let url = "https://free.currencyconvertapi.com/api/v5/convert?q=" + de_para + "L&compact=y";
      fetch(url).then(res => { return res.json() })
        .then(json => {
          let cotacao = json[de_para].val;
          this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2);
        })
    }
  }
}
</script>

<style scroped>
.conversor {
  padding: 20px;
  max-width: 300px;
  box-shadow: 0px 0px 10px #ccc;
}

.textcenter {
  text-align: center;
}
</style>