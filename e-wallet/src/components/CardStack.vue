<template>
  <div>
    <div v-if="empty"><h2 class="emptyText"><u>Your wallet is empty</u></h2></div>
    <div v-else>
      <Card
        :id="selected.id"
        :holder="selected.holder"
        :validMonth="selected.validMonth"
        :validYear="selected.validYear"
        :vendor="selected.vendor"
        :index="index"
      />
      <div class="cardStack">
        <div
          v-for="(card, index) of data"
          :key="index"
          @click="changeCard(index)"
        >
          <Card
            :id="card.id"
            :holder="card.holder"
            :validMonth="card.validMonth"
            :validYear="card.validYear"
            :vendor="card.vendor"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from "../components/Card.vue";
export default {
  name: "CardStack",
  components: { Card },
  data() {
    return {
      data: [],
      selected: {},
      index: 0,
      empty: false
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    changeCard(index) {
      this.selected = this.$root.$data.cards[index];
      this.index = index;
    },
    getData() {
      if (this.$root.$data.cards[0] == null) {
        this.empty = true;
      } else {
        this.data = this.$root.$data.cards;
        this.selected = this.$root.$data.cards[0];
        this.empty = false;
      }
    }
  }
};
</script>

<style>
.cardStack {
  margin-top: 35px;
  display: grid;
  grid-template-columns: auto;
  grid-auto-rows: 60px;
  grid-gap: 5px;
}
.emptyText{
  padding-top: 40px;
}
</style>
