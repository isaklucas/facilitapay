<template>
    <div class="header">

        <div class="conteudo">
            <div class="logo">
                <img src="https://static.wixstatic.com/media/56d601_9aaf731636ee47b1b717f56ee734898f~mv2.png/v1/fill/w_158,h_53,al_c,q_85,usm_0.66_1.00_0.01/fpay_logo.webp" alt="Facilita Pay Logo">
            </div>

            <nav>
                <ul>
                    <li><a href="#">Home</a></li>
                    <li><a href="#">Sobre Nós</a></li>
                    <li><a href="#">Como Funciona</a></li>
                    
                </ul>
            </nav>

           
        </div>
    </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({});
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



.logo{
    margin: 10px 0px 0px 35px;
    float: left;
}
nav li {
    list-style-type: none;
}

nav li a {
    text-decoration: none;
    line-height: 45px;
    margin-right: 40px;
    font-size: 1.2rem;
}

nav ul {
    display: flex;
    float: right;
    
    
}


/* Responsive */

@media screen and (max-width: 910px){

nav ul {
    display: none !important;
}
}
</style>