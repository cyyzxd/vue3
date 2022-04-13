<template>
  <HelloWorld @hello="showhello" msg="你好哇" school="abc">
    <template v-slot:zxd>
      <div>123</div>
    </template>
  </HelloWorld>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  setup() {
    function showhello(value) {
      console.log({ value });
    }

    return {
      showhello,
    };
    // console.log("---setup---");
  },
  components: {
    HelloWorld,
  },
};
</script>

<style></style>
