<script>
export default {
  name: 'StepOne',
  props: {
    formattedList: Array,
  },
  methods: {
    formatList: function (list) {
      this.$emit('formatList', list)
    },
  },
  data() {
    return {
      list: "BABA HOJE: \n" +
          "1- Arilson \n" +
          "2- jhone \n" +
          "3- Mário \n" +
          "4- Carlos\n" +
          "5- Murilo\n" +
          "6- Pedro\n" +
          "7- Thalys\n" +
          "8- Felipe Victor \n" +
          "9-Joao pedro\n" +
          "10- Wallace\n" +
          "11- Daniel\n" +
          "12- Lucas\n" +
          "13- Bernardo\n" +
          "14- Vinicius \n" +
          "15- Zé Vitor \n" +
          "16- Ellias \n" +
          "17- Yan georgi\n" +
          "18- Yan \n" +
          "19- Vitor \n" +
          "20- Iago \n" +
          "\n" +
          "Goleiros 🧤\n" +
          "1- Arthur \n" +
          "2- Franklin"
    }
  },
}
</script>

<template>
  <div class="mb-3">
    <label for="exampleFormControlTextarea1" class="form-label">Lista:</label>
    <textarea class="form-control" id="exampleFormControlTextarea1" rows="10" v-model="list"></textarea>
    <div class="col-12 mt-3">
      <a class="offset-4 col-4 bn39" @click="formatList(list)"><span class="bn39span">Começar</span></a>
    </div>
  </div>

</template>

<style>

</style>