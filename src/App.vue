<template>
  <div class="wrapper">
    <div class="general-title">
      Вентилятор
    </div>
    <div class="power__title">
      Мощность
    </div>
    <label>
      <input v-model="formData.power" @input="submit" class="power__console">
      кВт
    </label>
    <div class="director__title">
      Управление
    </div>
    <div class="director__console">
      <label v-for="(console, ind) of formShells.directorTypes" :key="ind + 'directorTypes'">
        <input type="radio" :value="console.value" v-model="formData.directorType" @click="submit">
        {{console.name}}
      </label>
    </div>
    <div class="options-title">
      Общие
    </div>
    <div class="shell__title">
      Корпус
    </div>
    <div class="shell__console">
      <label v-for="(console, ind) of formShells.shellTypes" :key="ind + 'shellTypes'">
        <input type="radio" :value="console.value" v-model="formData.shellType" @click="submit">
        {{console.name}}
      </label>
    </div>
    <div class="additional__title">
      Доп. опции
    </div>
    <div class="additional__console">
      <label>
        <input type="checkbox">
      </label>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    formData: {
      power: '2,2',
      directorType: 'switchDirectly',
      shellType: 'plastic',
    },
    formShells: {
      directorTypes: [
        {
          name: 'Прямой пуск',
          value: 'switchDirectly'
        },
        {
          name: 'Преобразователь частоты',
          value: 'frequenceConverter'
        }
      ],
      shellTypes: [
        {
          name: 'Пластик',
          value: 'plastic'
        },
        {
          name: 'Металл',
          value: 'iron'
        }
      ]
    }
  }),
  methods: {
    submit() {
      console.log('parameters =', this.formData)
      let toSend = JSON.stringify(this.formData)   //toSend отсылаем на сервер.
    }
  }
}
</script>

<style lang="scss">
.wrapper {
  max-width: 400px;
  margin: 60px auto;
  border: cadetblue 1px solid;
  
  display: grid;
  
}
</style>
