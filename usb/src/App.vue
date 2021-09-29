<template>
  <div class="app">
    <label for="vendorId">Vendor ID: 0x</label>
    <input
      type="text"
      name="vendorId"
      placeholder="vendorId"
      id="vendor"
      value="2a03"
    />
    <p>
      <a href="#" id="click" @click="click">Click me to get USB device info</a>
    </p>
    <!-- <div v-for="test in devices" :key="test.length" class="helloworld">
      <HelloWorld
        v-for="helloworld in device"
        :key="helloworld.productId"
        :name="helloworld.productName"
      ></HelloWorld>
    </div> a approfondir -->
    <HelloWorld
      v-for="helloworld in devices"
      :key="helloworld.productId"
      :name="helloworld.productName"
    ></HelloWorld>
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
  data() {
    return {
      devices: 0,
      device: "",
    };
  },
  methods: {
    click: function () {
      var vendorId = "0x" + document.getElementById("vendor").value;
      navigator.usb
        .requestDevice({ filters: [{ vendorId: vendorId }] })
        .then((device) => {
          console.log(device);
          console.log("Product ID: " + device.productId.toString(16));
          console.log("Vendor ID: " + device.vendorId.toString(16));
        })
        .catch((error) => {
          console.log(error);
        });
      navigator.usb.getDevices().then((devices) => {
        this.devices = devices.length;
        console.log("Total devices: " + devices.length);
        devices.forEach((device) => {
          this.device = device.productName;
          console.log(
            "Product name: " +
              device.productName +
              ", serial number " +
              device.serialNumber
          );
        });
      });
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

.hellorworld {
}
</style>
