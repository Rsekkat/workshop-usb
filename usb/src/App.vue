<template>
  <div id="app" class="app">
    <a href="#" id="display" @click="connect_usb"> Connection to usb device </a>
    <p id="display"></p>
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
      navigator.usb.getDevices().then((devices) => {
        console.log("Total devices: " + devices.length);
        devices.forEach((device) => {
          console.log(
            "Product name: " +
              device.productName +
              ", serial number " +
              device.serialNumber
          );
        });
      });
    },
    test: function () {
      var usb = require("usb");
      document.getElementById("display").innerHTML = JSON.stringify(
        usb.getDeviceList()
      );
      console.log(usb.getDeviceList());
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
