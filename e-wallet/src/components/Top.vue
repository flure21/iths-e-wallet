<template>
  <header>
    <h1>{{ Heading }}</h1>
    <h4>{{ SubHeading }}</h4>
  </header>
</template>

<script>
export default {
  name: "Top",
  props: {
    Heading: String,
    SubHeading: String
  }
};
</script>

<style></style>
