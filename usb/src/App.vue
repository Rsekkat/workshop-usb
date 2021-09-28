<template>
  <div id="app" class="app">
    <a href="#" id="click" @click="connect_usb"> Connection to usb device </a>
    <HelloWorld name="test"></HelloWorld>
  </div>
</template>
<script>
//import Vue from "vue";
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  methods: {
    connect_usb: function () {
      // PROBLEME AVEC CETTE TECHNIQUE C'EST QU'IL FAUT RECCUPÉRER LE VENDORID MAIS IL DOIT Y AVOIR UNE AUTRE SOLUTION
      navigator.usb
        .requestDevice({ filters: [{ vendorId: 0x2109 }] })
        .then((device) => {
          console.log(device);
          console.log(device.productId.toString(16));
          console.log(device.vendorId.toString(16));
        })
        .catch((error) => {
          console.log(error);
        });
    },
    test: function () {
      var usb = require('usb')
      document.getElementById("display").innerHTML = JSON.stringify(
        usb.getDeviceList()
      );
    },
  },
};
var OS = "OS Inconnu";
if (navigator.appVersion.indexOf("Win") != -1) OS = "Windows";
if (navigator.appVersion.indexOf("Mac") != -1) OS = "MacOS";
if (navigator.appVersion.indexOf("X11") != -1) OS = "Unix";
if (navigator.appVersion.indexOf("Linux") != -1) OS = "Linux";
console.log(OS);
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.app {
  display: flex;
  justify-content: center;
}
</style>
