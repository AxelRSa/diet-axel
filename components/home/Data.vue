<template lang="pug">
div
  form
    label Peso:
    input(type="number" v-model="weight" @change="calculations()")
    label Altura:
    input(type="number" v-model="height" @change="calculations()")
    label Años:
    input(type="number" v-model="age" @change="calculations()")
    label ¿Cuántos días a la semana haces más de 40 minutos de actividad física?
    select(v-model="levelOfActivity" @change="calculations()")
      option(value="1.2") 0
      option(value="1.38") 1 - 3
      option(value="1.55") 3 - 5
      option(value="1.73") 6 - 7
      option(value="1.90") Atleta profesional
  p Calorías para mantenerse: {{ caloriesMantein }}
  p Índice de masa corporal(IMC): {{ bodyMassindex }}
  table
    tr
      th IMC
      th Nivel de peso
    tr
      td <18.5
      td Bajo Peso
    tr
      td 18.5 - 24.9
      td Normal
    tr
      td 25.0 - 29.9
      td Sobrepeso
    tr
      td 30.0 o más
      td Obeso

</template>

<script>
export default {
  data() {
    return {
      weight: 105,
      height: 179,
      age: 25,
      levelOfActivity: 1.2,
      caloriesMantein: 0,
      bodyMassindex: 0,
    }
  },
  computed: {
    toFloatLevelOfActivity() {
      return parseFloat(this.levelOfActivity)
    },
    toFloatWeight() {
      return parseFloat(this.weight)
    },
    toFloatHeight() {
      return parseFloat(this.height)
    },
    toFloatAge() {
      return parseFloat(this.age)
    },
  },
  mounted() {
    this.calculations()
  },
  methods: {
    calculations() {
      this.calculateCaloriesMantein()
      this.calculateBodyMassindex()
    },
    calculateCaloriesMantein() {
      this.caloriesMantein = Math.round(
        (this.toFloatWeight * 10 +
          this.toFloatHeight * 6.25 +
          this.toFloatAge * 5 +
          5) *
          this.toFloatLevelOfActivity
      )
    },
    calculateBodyMassindex() {
      this.bodyMassindex = Math.round(
        this.toFloatWeight /
          ((this.toFloatHeight / 100) * (this.toFloatHeight / 100))
      )
    },
  },
}
</script>
<style lang="scss" scoped>
form > label,
input {
  display: block;
}
table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
}
</style>
