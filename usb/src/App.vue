<template>
  <div class="app">
    <div>
      To find your vendor ID, go to this link: "about://usb-internals" and click on "device" to see all your device connected 
    </div>
    <label for="vendorId">Vendor ID: 0x</label>
    <input
      type="text"
      name="vendorId"
      placeholder="vendorId"
      id="vendor"
      value="2a03"
      class="input"
    />
    <div class="button">
      <a href="#" id="click" @click="click">Add USB</a>
    </div>
    <div class="helloworld">
      <HelloWorld
        v-for="helloworld in devices"
        :key="helloworld.productId"
        :name="device.productName"
      ></HelloWorld>
    </div>
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
      device: [],
      productName: "",
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
          this.device = device;
          this.productName = device.productName;
          console.log(
            "Product name: " +
              device.productName +
              ", serial number " +
              device.serialNumber
          );
        });
      });
    },
    click2: function () {},
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

.button {
  display: flex;
  align-items: center;
  width: 220px;
  height: 40px;
  padding: 7px 75px 9px;
  border-radius: 4px;
  background-color: black;
  margin: 10px;
}

.button a {
  color: white;
  text-decoration: none;
}

.input {
  width: 10%;
  border-radius: 5px;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
}

.app {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 100%;
  align-items: center;
}

.helloworld {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
