<script >
  export default {
    data() {
      return {
        matrix_desordenada: '',
        matrix_ordenada: ''
      }
    },
    methods: {
      reformat_matrix(matrix){
        matrix = matrix.replace('[', "")
        matrix = matrix.replace(']', "")
        var arr = matrix.split(",")
        var array_positive_matrix = arr.map((num) => parseInt(num));
        return array_positive_matrix
      },
      positive_matrix(matrix) {
        var new_array_positive_matrix = matrix.filter((num) => num >= 0);
        return new_array_positive_matrix
      },
      negative_matrix(matrix) {
        var new_array_negative_matrix = matrix.filter((num) => num < 0);
        return new_array_negative_matrix
      },
      result_matrix(matrix) {
        var a = this.positive_matrix(matrix);
        var b = this.negative_matrix(matrix);
        return [...a, ...b]
        
      },
      submit(e) {
        console.log(this.matrix_desordenada);
        e.preventDefault();  
        this.matrix_ordenada = this.result_matrix(this.reformat_matrix(this.matrix_desordenada));
      },
    }
  };
</script>

<template>
  <div class="h-screen flex items-center justify-center">
    <form v-on:submit="submit" class="w-full max-w-sm">
      <div class="w-full">
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
            type="text" 
            placeholder="matrix"
            v-model="matrix_desordenada"/>
      </div>
      <div class="flex flex-col items-center">
      <button class="bg-blue-500 hover:bg-blue-700 text-center text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" 
        type="submit">
        Ordenar Matrix
      </button>
      <br>
      <p>{{ matrix_ordenada }}</p>
      </div>
    </form>
  </div>
</template>