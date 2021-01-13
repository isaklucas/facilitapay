<template>
  <div class="header">
    <div class="conteudo">
      <div class="logo">
        <img
          src="https://static.wixstatic.com/media/56d601_9aaf731636ee47b1b717f56ee734898f~mv2.png/v1/fill/w_158,h_53,al_c,q_85,usm_0.66_1.00_0.01/fpay_logo.webp"
          alt="Facilita Pay Logo"
        />
      </div>

      <nav>
        <ul>
          <li><a href="#">Home</a></li>
          <li><a href="#">Sobre Nós</a></li>
          <li><a href="#">Como Funciona</a></li>
          <li class="butao">
            <v-btn rounded dark>
              Login
              <v-icon class="icone" medium color="green darken-2">
                mdi-login
              </v-icon>
            </v-btn>
          </li>
        </ul>
      </nav>

      <div class="mobilemenu">
        <v-menu>
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark v-bind="attrs" v-on="on">
              <v-icon class="icone" medium>
                mdi-menu
              </v-icon>
            </v-btn>
          </template>

          <v-list>
            <v-list-item v-for="(item, index) in items" :key="index">
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  data: () => ({
    items: [
      { title: "Home" },
      { title: "Sobre Nós" },
      { title: "Como Funciona" },
      { title: "Login" },
    ],
  }),
});
</script>

<style lang="css" scoped>
.header {
  width: 100%;
  background-color: white;
}

.conteudo {
  width: 1280px;
  margin: 0 auto;
  font-size: 10px;
  height: 80px;
}

.logo {
  margin: 10px 0px 0px 35px;
  float: left;
}
nav li {
  list-style-type: none;
}

nav li a {
  text-decoration: none;
  line-height: 80px;
  margin-right: 40px;
  font-size: 1.2rem;
  color: black;
}

nav ul {
  display: flex;
  float: right;
}

.butao {
  margin-top: 20px;
}

.butao .icone {
  margin-left: 3px;
}

.mobilemenu {
  display: none;
}

/* Responsive */

@media screen and (max-width: 1280px) {
  .conteudo {
    width: 100%;
  }
  nav ul {
    margin-right: 20px;
  }
}

@media screen and (max-width: 910px) {
  nav ul {
    display: none !important;
  }

  .conteudo {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .mobilemenu {
    display: block;
    margin-right: 40px;
  }

  @media (max-width: 305px) {
    .logo {
      margin: 0 0 0 10px;
    }

    .mobilemenu {
      margin-right: 10px;
      margin-bottom: 10px;
    }
  }
}
</style>
