<template>
  <div>
    <Card
      :id="add.id"
      :holder="add.holder"
      :validMonth="add.validMonth"
      :validYear="add.validYear"
      :vendor="add.vendor"
      class="mb"
    />
    <div class="formContainer">
      <label>CARD NUMBER</label>
      <input
        type="text"
        v-model="add.id"
        maxlength="16"
        placeholder="XXXX XXXX XXXX XXXX"
      />
    </div>
    <div class="formContainer">
      <label>CARDHOLDER NAME</label>
      <input
        type="text"
        v-model="add.holder"
        placeholder="Firstname Lastname"
        class="col-2"
      />
    </div>
    <div class="formDateContainer">
      <div class="date">
        <label>MONTH</label>
        <select v-model="add.validMonth">
          <option v-for="(month, index) in months" :key="index">
            {{ month }}
          </option>
        </select>
      </div>
      <div class="date">
        <label>YEAR</label>
        <select v-model="add.validYear">
          <option v-for="(year, index) in years" :key="index">
            {{ year }}
          </option>
        </select>
      </div>
    </div>
    <div class="formContainer">
      <label>VENDOR</label>
      <select v-model="vendorName" @change="changeTheme()">
        <option
          v-for="(vendor, index) in vendors"
          :key="index"
          :value="vendor.value"
        >
          {{ vendor.name }}
        </option>
      </select>
    </div>
    <div>
      <button class="addButton" @click="addCard">
        <span class="button-text">ADD CARD</span>
      </button>
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  name: "CardForm",
  components: { Card },
  data() {
    return {
      add: {
        id: "",
        holder: "",
        vendor: "add",
        validYear: "YY",
        validMonth: "MM"
      },
      months: [
        "01",
        "02",
        "03",
        "04",
        "05",
        "06",
        "07",
        "08",
        "09",
        "10",
        "11",
        "12"
      ],
      years: ["22", "23", "24", "25", "26"],
      vendors: [
        { name: "Bitcoin Inc", value: "bitcoin" },
        { name: "Blockchain Inc", value: "blockchain" },
        { name: "Evil Corp", value: "evil" },
        { name: "Ninja Bank", value: "ninja" }
      ],
      vendorName: ""
    };
  },
  methods: {
    changeTheme() {
      this.add.vendor = this.vendorName;
    },
    addCard() {
      this.$root.$data.cards.push(this.add);
      this.$router.push("/");
    }
  }
};
</script>

<style scoped>
.addButton {
  margin-top: 40px;
}
input,
select {
  font-size: 16px;
  padding: 8px;
  border-radius: 6px;
  border: 1px solid black;
}
.formContainer {
  display: flex;
  flex-direction: column;
  text-align: left;
  margin-bottom: 14px;
}
.formDateContainer {
  display: flex;
  width: 100%;
  gap: 20px;
  margin-bottom: 14px;
}
.date {
  display: flex;
  flex-direction: column;
  width: 100%;
  text-align: left;
}
.mb {
  margin-bottom: 30px;
}
</style>
