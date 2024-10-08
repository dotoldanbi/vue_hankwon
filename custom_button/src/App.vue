<template>
  <div>
    <MyButton type="switch" 
    background-blue text-white 
    v-model:active="active">SWITCH</MyButton>
  </div>
</template>

<script>
import MyButton from "./components/MyButton.vue";

export default {
  name: "App",
  methods: {
    onClick(evt) {
      alert("clicked");
    },
  },
  components: { MyButton },
};
</script>
