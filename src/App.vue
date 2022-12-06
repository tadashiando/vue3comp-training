<script setup>
  import { ref, computed } from 'vue'

  	const name = 'Vue dinámico'
  	
    let counter = ref(0);
    let isAddDisabled = ref(false);

    let arrayNumbers = ref([]);

    const increment = () => {
      counter.value++;
      checkArrayContainingNumber()
    }
    const decrement = () => {
      counter.value--;
      checkArrayContainingNumber()
    }
    const reset = () => {
      counter.value = 0;
      checkArrayContainingNumber()
    }
    
    const checkArrayContainingNumber = () => {
      if(arrayNumbers.value.includes(counter.value)) {
        isAddDisabled.value = true;
      } else {
        isAddDisabled.value = false;
      }
    }
    
    const add = () => {
      if(!isAddDisabled.value) {
        arrayNumbers.value.push(counter.value)
        checkArrayContainingNumber()
      }
    }

    const classCounter = computed(() => {
      if( counter.value < 0 ) {
        return 'negative';
      } else if (counter.value === 0) {
        return 'zero'
      }
      return 'positive'
    })
</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <br />
    <h2 :class="classCounter">{{ counter }}</h2>
    <br />
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Resetear</button>
      <button @click="add" :disabled="isAddDisabled" class="btn btn-primary">Add</button>  
    </div>
    <span>
      <ul class="list-group">
        <li v-for="item in arrayNumbers" class="list-group-item">{{item}}</li>
      </ul>
    </span>
  </div>
</template>

<style>
  h1 {
    color: brown;
  }

  .negative {
    color: red;
  }

  .positive {
    color: green;
  }

  .zero {
    color: blue;
  }
</style>