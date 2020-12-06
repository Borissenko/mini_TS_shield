<template>
  <div class="wrapper">
    <div class="topic">
      Вентилятор
    </div>
    <div class="power__title">
      Мощность
    </div>
    <label class="power__console">
      <input v-model="formData.power" @input="submit">
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
      <label v-for="(console, ind) of formShells.additionalTypes" :key="ind + 'additionalTypes'">
        <input type="checkbox" :value="console.value" v-model="formData.additionalTypes" @click="submit">
        {{console.name}}
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
      additionalTypes: ['fireAlert', 'LedIndication']
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
      ],
      additionalTypes: [
        {
          name: 'Сигнал "Пожар"',
          value: 'fireAlert'
        },
        {
          name: 'LED-индикация',
          value: 'LedIndication'
        },
        {
          name: 'Диспетчеризация',
          value: 'dispatching'
        }
      ]
    }
  }),
  methods: {
    submit() {
      if(this.formData.power.length === 0) return  //предотвращаем отправку при пустом поле "Мощность".
      console.log('parameters =', this.formData)
      let toSend = JSON.stringify(this.formData)   //отсылаем значение toSend на сервер.
    }
  }
}
</script>

<style lang="scss">
.general-title {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  font-weight: bold;
  color: chocolate;
}

.ff-row {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.ff-col {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
}

.title {
  font-weight: bold;
  color: cadetblue;
}

label {
  display: block;
  margin-right: 5px;
}

.wrapper {
  max-width: 400px;
  height: auto;
  margin: 60px auto;
  border: #e6e8e8 1px dashed;
  
  font-size: 16px;
  
  display: grid;
  grid-template-columns: 40% 60%;
  grid-auto-rows: 60px;
  
  @media (max-width: 400px) {  //адаптация на скрин, меньший 400px
    width: 300px;
    display: flex;
    flex-flow: column nowrap;
    align-items: center;
    justify-content: space-between;
  
    & :nth-child(n) {
      margin-bottom: 10px;
    }
  }
  
  .topic {
    grid-area: 1 / 1 / 1 / span 2;
    @extend .general-title;
  }
  
  .options-title {
    grid-area: 4 / 1 / 4 / span 2;
    @extend .general-title;
  }
  
  .power {
    &__title {
      grid-area: 2 / 1 / 2 / 1;
      @extend .title;
      @extend .ff-row;
    }
    
    &__console {
      grid-area: 2 / 2 / 2 / 2;
      @extend .ff-row;
      
      input {
        width: 40px;
        height: 30px;
        margin-right: 10px;
        padding-left: 10px;
      }
    }
  }
  
  .director {
    &__title {
      grid-area: 3 / 1 / 3 / 1;
      @extend .title;
      @extend .ff-row;
    }
    
    &__console {
      grid-area: 3 / 2 / 3 / 2;
      @extend .ff-col;
    }
  }
  
  .shell {
    &__title {
      grid-area: 5 / 1 / 5 / 1;
      @extend .title;
      @extend .ff-row;
    }
    
    &__console {
      grid-area: 5 / 2 / 5 / 2;
      @extend .ff-col;
    }
  }
  
  .additional {
    &__title {
      grid-area: 6 / 1 / 6 / 1;
      @extend .title;
      @extend .ff-row;
      align-items: flex-start;
    }
    
    &__console {
      grid-area: 6 / 2 / 6 / 2;
    }
  }
}
</style>
