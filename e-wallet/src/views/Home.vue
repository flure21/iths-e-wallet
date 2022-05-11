<template>
  <div>
    <Top :Heading="'E-WALLET'" :SubHeading="'ACTIVE CARD'" />
    <CardStack />
    <button v-on:click="addCard">
      <span class="buttonText">ADD NEW CARD</span>
    </button>
  </div>
</template>

<script>
import Top from "../components/Top.vue";
import CardStack from "../components/CardStack.vue";
export default {
  name: "Home",
  components: {
    Top,
    CardStack
  },
  methods: {
    addCard() {
      this.$router.push("/addcard");
    }
  }
};
</script>
<style>
button {
  width: 100%;
  border: 2px solid black;
  border-radius: 10px;
  height: 60px;
  background-color: white;
  margin-top: 200px;
}
button:hover {
  background-color: black;
  color: white;
  cursor: pointer;
}
.buttonText {
  font-size: large;
}
</style>
