<template>
  <div>
    <div class="deletePopup" v-if="popup == true">
      <div class="deletePopupWindow">
        <div class="deleteButton" @click="closePopup()">X</div>
        <h2>
          Do you really want to
          <span class="red">delete</span>?
        </h2>
        <div class="deletePopupButton" @click="deleteCard()">
          <span>DELETE</span>
        </div>
      </div>
    </div>
    <div class="card" :class="vendor">
      <div class="images">
        <div class="imageLeft">
          <span
            v-show="index !== undefined"
            class="deleteButton"
            @click="deletePopup(index)"
            >X</span
          >
          <img
            v-if="
              vendor === 'ninja' || vendor === 'blockchain' || vendor === 'evil'
            "
            class="chip"
            height="80"
            src="../assets/chip-light.svg"
          />
          <img
            v-if="vendor === 'bitcoin' || vendor === 'add'"
            class="chip"
            height="80"
            src="../assets/chip-dark.svg"
          />
        </div>
        <img
          v-if="vendor === 'bitcoin'"
          height="40"
          src="../assets/vendor-bitcoin.svg"
        />
        <img
          v-if="vendor === 'blockchain'"
          height="40"
          src="../assets/vendor-blockchain.svg"
        />
        <img
          v-if="vendor === 'ninja'"
          height="40"
          src="../assets/vendor-ninja.svg"
        />
        <img
          v-if="vendor === 'evil'"
          height="40"
          src="../assets/vendor-evil.svg"
        />
      </div>
      <div class="number">
        <span v-html="$options.filters.splitId(id)"></span>
      </div>
      <div class="info">
        <div class="name">
          <p class="smallText">CARDHOLDER NAME</p>
          <p class="mediumText">{{ holder }}</p>
        </div>
        <div class="valid">
          <p class="smallText">VALID UNTIL</p>
          <p class="mediumText">{{ validMonth }}/{{ validYear }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    id: String,
    holder: String,
    validYear: String,
    validMonth: String,
    vendor: String,
    index: Number,
  },
  data() {
    return {
      popup: false,
      deleteId: 0,
    };
  },
  filters: {
    splitId: function (value) {
      if (!value) return "";
      const first = value.substring(0, 4);
      const second = value.substring(4, 8);
      const third = value.substring(8, 12);
      const forth = value.substring(12, 16);
      const id = first + " " + second + " " + third + " " + forth;
      return id;
    },
  },
  methods: {
    deletePopup(index) {
      this.popup = true;
      if (this.$root.$data.cards.length == 1) {
        this.deleteId = 0;
      } else {
        this.deleteId = index;
      }

      console.log(index);
    },
    closePopup() {
      this.popup = false;
    },
    deleteCard() {
      this.$root.$data.cards.splice(this.deleteId, 1);
      this.$parent.getData();
      this.deleteId = 0;
      this.popup = false;
    },
  },
};
</script>

<style>
.card {
  display: flex;
  width: 95%;
  margin: auto;
  border-radius: 8px;
  box-shadow: 0 0 0.5rem rgb(0 0 0 / 40%);
  padding: 10px;
  flex-direction: column;
}
.bitcoin {
  background-color: rgb(255, 174, 52);
  color: black;
}
.blockchain {
  background-color: #8b58f9;
  color: white;
}
.ninja {
  background-color: #222;
  color: white;
}
.evil {
  background-color: rgb(243, 51, 85);
  color: white;
}
.add {
  background-color: rgb(208, 208, 208);
  color: black;
}
.images {
  display: flex;
  justify-content: space-between;
}
.number {
  font-size: 30px;
  padding-top: 15px;
  text-align: left;
  height: 36px;
}
.chip {
  padding-top: 30px;
}
.info {
  display: flex;
  margin-top: 15px;
}
.name {
  display: flex;
  flex-direction: column;
  width: 80%;
}
.valid {
  display: flex;
  flex-direction: column;
  width: 20%;
}
.name > p {
  width: 100%;
  margin: 2px 0 2px 0;
  padding: 0;
  text-align: left;
}
.valid > p {
  width: 100%;
  margin: 2px 0 2px 0;
  padding: 0;
  text-align: right;
}
.smallText {
  font-size: 10px;
}
.mediumText {
  font-size: 16px;
}
.imageLeft {
  display: flex;
}
.deleteButton {
  font-size: 18px;
  font-weight: bolder;
  cursor: pointer;
  text-align: right;
  margin-right: 10px;
}
.deletePopup {
  z-index: 1;
  position: fixed;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  background-color: rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
}
.deletePopupWindow {
  width: 300px;
  height: 170px;
  border: white 1px solid;
  border-radius: 10px;
  background-color: white;
}
.red {
  color: red;
}
.deletePopupButton {
  width: 100px;
  height: 35px;
  margin: auto;
  border: #222 solid 1px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
}
.deletePopupButton:hover {
  background-color: red;
  color: white;
  cursor: pointer;
  border-color: white;
}
</style>
