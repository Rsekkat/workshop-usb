<template>
  <div class="BG">
    <ul>
      <li>
        <a>{{ name }}</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    name: {
      type: String,
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.BG {
  display: flex;
  align-items: center;
  width: 80%;
  height: 70px;
  padding: 15px;
  margin-top: 14px;
  background-color: white;
  border-radius: 5px;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
}
li{
  list-style-type: none; 
}
</style>
