<template>
  <div class="conteiner">
    <div class="envia">
      <input type="number" v-model="envia" placeholder="Voce Envia" />
      <select v-model="selecionadoE">
        <option value="BRL"> BRL</option>
        <option value="USD">USD</option>
        <option value="EUR">EUR</option>
      </select>
    </div>

    <div class="taxas">
      <ul>
        <span></span>
        <li>{{ selecionadoE }} 1 = {{selecionadoR}} {{taxa}}</li>
        <span></span>
        <li>IOF (1.10%) = {{ selecionadoE }} {{ calculoiof }}</li>
        <span></span>
        <li>
          Taxa administrativa = {{ selecionadoE }} {{ calculofx }}
        </li>
      </ul>
    </div>

    <div class="recebe">
      <input
        v-model="valorconvertido"
        type="number"
        placeholder="beneficiario recebe"
      />
      <select v-model="selecionadoR" name="MoedasR" id="MoedaR">
        <option value="BRL">BRL</option>
        <option value="USD">USD</option>
        <option value="EUR">EUR</option>
      </select>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  
    
  
  
  data() {
    return {
      envia: 0,
      selecionadoE: "BRL",
      selecionadoR: "EUR",
    };
  },
  computed: {

    calculoiof() {
      return this.envia * 0.011;
    },
    calculofx() {
      return this.envia * 0.01;
    },

    taxa() {
      if (
        this.selecionadoE == "USD" &&
        this.selecionadoR == "BRL"
      ) {
        return 5.2164;
      }
      if (
        this.selecionadoE == "BRL" &&
        this.selecionadoR == "USD"
      ) {
        return 0.1917;
      } 
      if (
        this.selecionadoE == "EUR" &&
        this.selecionadoR == "BRL"
      ) {
        return 6.3970;
      }
      if (
        this.selecionadoE == "BRL" &&
        this.selecionadoR == "EUR"
      ) {
        return 0.1563;
      }
      if (
        this.selecionadoE == "EUR" &&
        this.selecionadoR == "USD"
      ) {
        return 1.2206;
      }
      if (
        this.selecionadoE == "USD" &&
        this.selecionadoR == "EUR"
      ) {
        return 0.8192;
      }
      else return 1;
    },

    valorconvertido() {
        console.log(this)
      return (
        (this.envia -
          this.calculoiof -
          this.calculofx) *
        this.taxa
      );
    },
  },
});
</script>

<style lang="css">
.conteiner {
  width: 1280px;
  margin: 0 auto;
}

.envia {
  width: 525px;
  margin: 100px auto 0px;
  background-color: skyblue;
  box-shadow: 0px 1px 5px black;
  border-radius: 8px;

  overflow: hidden;
}

.envia input {
  height: 45px;
  width: 400px;
  float: left;
}

.envia select {
  height: 45px;
  width: 120px;
  float: left;
}

.taxas {
  width: 525px;
  margin: 0 auto;

  clear: both;

  color: white;
}

.recebe {
  width: 525px;
  margin: 0 auto;

  background-color: skyblue;
  box-shadow: 0px 1px 5px black;

  border-radius: 8px;

  overflow: hidden;
}

.recebe input {
  height: 45px;
  width: 400px;
  float: left;
}

.recebe select {
  height: 45px;
  width: 120px;
  float: left;
}

input {
  border-radius: 8px;
  border: none;
}

select {
  background-color: skyblue;
  color: white;
  border: none;
}

.flags {
  width: 45px;
  height: 45px;

  clear: both;
}

span:before {
  content: "";
  position: absolute;
  width: 2px;
  height: 106px;
  border: 0 solid;
  border-color: inherit;
  outline: 0;
  background-color: white;
  background-size: 200% 200%;
  background-position: 0 0;
  top: 226px;
  margin-left: 9px;
}

span {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: white;
  display: block;
  float: left;
}

.taxas li {
  list-style-type: none;
  line-height: 25px;
  margin-left: 40px;
}
</style>
