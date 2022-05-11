<template>
  <div>
    <Top :Heading="'ADD NEW CARD'" :SubHeading="'NEW CARD'" />
    <CardForm />
  </div>
</template>

<script>
import Top from "../components/Top.vue";
import CardForm from "../components/CardForm.vue";
export default {
  name: "AddCard",
  components: {
    Top,
    CardForm
  },
  data() {
    return {};
  }
};
</script>

<style></style>
