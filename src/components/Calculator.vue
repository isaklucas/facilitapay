<template>
  <div>
    <v-app class="container">
      <div class="enviaform">
        <div>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field-money
              v-model="valorInicial"
              label="Você Envia"
              :properties="{
                prefix: currency,
                readonly: false,
                disabled: false,
                outlined: false,
                clearable: true,
                placeholder: ' ',
              }"
              :options="{
                locale: 'pt-BR',
                length: 111,
                precision: 2,
                empty: null,
              }"
            />
          </v-form>
        </div>

        <div class="v-select-img">
          <i v-if="select" :class="['mr-2', 'em', flag]"></i>
          <v-select
            class="custom"
            v-model="select"
            :items="countries"
            label="Moeda Origem"
            item-text="name"
            item-value="name"
            return-object
            single-line
            text-color="white"
          >
            <template v-slot:item="slotProps">
              <i :class="['mr-2', 'em', slotProps.item.flag]"></i>
              {{ slotProps.item.name }}
            </template>
          </v-select>
        </div>
      </div>

      <div class="taxas">
        <ul>
          <span class="linha"></span>
          <li>{{ selectname }} 1 = {{ selectname2 }} {{ taxa }}</li>
          <span></span>
          <li>IOF (1.10%) = {{ selectname }} {{ maskiof }}</li>
          <span></span>
          <li>Taxa administrativa = {{ selectname }} {{ maskfx }}</li>
        </ul>
      </div>

      <div class="recebeform">
        <div>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field-money
              v-model="valorconvertido"
              label="Beneficiário Recebe"
              :properties="{
                prefix: currency2,
                readonly: false,
                disabled: false,
                outlined: false,
                clearable: true,
                placeholder: ' ',
              }"
              :options="{
                locale: 'pt-BR',
                length: 111,
                precision: 2,
                empty: null,
              }"
            />
          </v-form>
        </div>

        <div class="v-select-img">
          <i v-if="select2" :class="['mr-2', 'em', flag2]"></i>
          <v-select
            v-model="select2"
            :items="countries2"
            label="Moeda Destino"
            item-text="name"
            item-value="name"
            return-object
            single-line
          >
            <template v-slot:item="slotProps">
              <i :class="['mr-2', 'em', slotProps.item.flag]"></i>
              {{ slotProps.item.name }}
            </template>
          </v-select>
        </div>
      </div>
    </v-app>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  data: () => {
    return {
      envia: 0,
      valid: true,
      valorInicial: 0,
      select: { name: "USD", flag: "em-flag-us", value: "USD" },
      select2: { name: "BRL", flag: "em-flag-br", value: "BRL" },
      countries: [
        {
          name: "USD",
          flag: "em-flag-us",
          value: "USD",
        },
        {
          name: "EUR",
          flag: "em-flag-eu",
          value: "EUR",
        },
        {
          name: "BRL",
          flag: "em-flag-br",
          value: "BRL",
        },
      ],
      countries2: [
        {
          name: "USD",
          flag: "em-flag-us",
          value: "USD",
        },
        {
          name: "EUR",
          flag: "em-flag-eu",
          value: "EUR",
        },
        {
          name: "BRL",
          flag: "em-flag-br",
          value: "BRL",
        },
      ],
    };
  },
  computed: {
    selectname(): string {
      let name = "";
      if (this.select?.name == "BRL") name = "BRL";
      if (this.select?.name == "EUR") name = "EUR";
      if (this.select?.name == "USD") name = "USD";
      return name;
    },
    selectname2(): string {
      let name2 = "";
      if (this.select2?.name == "BRL") name2 = "BRL";
      if (this.select2?.name == "EUR") name2 = "EUR";
      if (this.select2?.name == "USD") name2 = "USD";
      return name2;
    },
    currency(): string {
      let valor = "";
      if (this.select?.name == "BRL") valor = "R$";
      if (this.select?.name == "EUR") valor = "€";
      if (this.select?.name == "USD") valor = "$";
      return valor;
    },
    flag() {
      return this.select?.flag || "";
    },
    currency2(): string {
      let valor = "";
      if (this.select2?.name == "BRL") valor = "R$";
      if (this.select2?.name == "EUR") valor = "€";
      if (this.select2?.name == "USD") valor = "$";
      return valor;
    },
    flag2() {
      return this.select2?.flag || "";
    },
    calculoiof(): number {
      return this.valorInicial * 0.011;
    },
    calculofx(): number {
      return this.valorInicial * 0.01;
    },
    maskiof(): string {
      return this.calculoiof.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      });
    },
    maskfx(): string {
      return this.calculofx.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      });
    },
    taxa(): number {
      if (this.select?.value == "USD" && this.select2?.value == "BRL") {
        return 5.2164;
      }
      if (this.select?.value == "BRL" && this.select2?.value == "USD") {
        return 0.1917;
      }
      if (this.select?.value == "EUR" && this.select2?.value == "BRL") {
        return 6.397;
      }
      if (this.select?.value == "BRL" && this.select2?.value == "EUR") {
        return 0.1563;
      }
      if (this.select?.value == "EUR" && this.select2?.value == "USD") {
        return 1.2206;
      }
      if (this.select?.value == "USD" && this.select2?.value == "EUR") {
        return 0.8192;
      } else return 1;
    },
    valorconvertido(): number {
      return (this.valorInicial - this.calculoiof - this.calculofx) * this.taxa;
    },
  },
});
</script>
<style lang="css" scoped>
.v-application {
  background-color: transparent !important;
}

.enviaform,
.recebeform {
  height: 60px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 680px;
  margin: 0 auto 30px;
  border-radius: 10px;
}

.enviaform {
  margin-top: 100px;
}
.v-form {
  color: #fff;
  margin-right: 20px;
  width: 160%;
  padding: 3px 30px 0px 3px;

  border-radius: 8px;
  box-sizing: border-box;

  background-color: #fff;
}
.v-select-img {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #7f93b7;

  z-index: 10;
  height: 74px;
  border-radius: 0 8px 8px 0;
  padding: 10px;
}
.v-select {
  width: 130px;

  border-radius: 8px;

  box-sizing: border-box;
}

.taxas {
  margin-bottom: 30px;
  color: #fff;
  margin: 0 auto 30px;
  width: 540px;
}

.linha:before {
  content: "";
  position: absolute;
  width: 3px;
  height: 135px;
  border: 0 solid;
  border-color: inherit;
  outline: 0;
  background-color: white;
  background-size: 200% 200%;
  background-position: 0 0;
  top: 160px;
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

.v-select__selection {
  color: #fff !important;
}

@media (max-width: 700px) {
  .enviaform,
  .recebeform {
    width: 90%;
    display: flex;
    justify-content: space-around;
  }

  .v-form {
    width: 137%;
    padding-right: 150px;
  }

  .v-select-img {
    width: 30%;
    padding-left: 5px;
    height: 75px;
  }

  .taxas {
    width: 85%;
  }

  @media (max-width: 421px) {
    .taxas {
      width: 95%;
    }
  }

  @media (max-width: 305px) {
    .taxas {
      width: 100%;
      font-size: 0.9rem;
    }
  }
}
</style>
