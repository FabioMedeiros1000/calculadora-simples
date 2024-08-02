<script setup>
import { reactive } from 'vue';

  const estado = reactive(
    {
      'numero1': 1,
      'numero2': 1,
      'operacao': 'adicao',
      'resultado': 2
    }
  )

  const retornaResultado = () => {
    if ((estado.resultado % 1) === 0){
      return estado.resultado;
    }
    else{
      return parseFloat(estado.resultado.toFixed(3));
    }
  }

  const somar = () => {
    estado.resultado = parseFloat(estado.numero1) + parseFloat(estado.numero2);
    return retornaResultado();
  }

  const subtrair = () => {
    estado.resultado = parseFloat(estado.numero1) - parseFloat(estado.numero2);
    return retornaResultado();
  }

  const multiplicar = () => {
    estado.resultado = parseFloat(parseFloat(estado.numero1) * parseFloat(estado.numero2));
    return retornaResultado();
  }

  const dividir = () => {
    if (parseFloat(estado.numero2) == 0){
      return 'infinito';
    }else{
      estado.resultado = (estado.numero1) / parseFloat(estado.numero2);
      return retornaResultado();
    }
  }

  const realizaOperacao = () => {
    switch (estado.operacao){
      case 'adicao':
        return somar();
      case 'subtracao':
        return subtrair();
      case 'multiplicacao':
        return multiplicar();
      case 'divisao':
        return dividir();
    }
  }
</script>

<template>
  <div class="container">
    <h1 class="pt-5 pb-3">Calculadora simples</h1>
    <p>Digite abaixo os números e a operação desejada</p>
    <form class="form">
      <div class="row">
        <div class="col-md-2 col-5">
          <input @keyup="evento => estado.numero1 = evento.target.value" type="number" value="1" placeholder="Primeiro número" class="form-control">
        </div>
        <div class="col-md-2 col-5">
          <input @keyup="evento => estado.numero2 = evento.target.value" type="number" value="1" placeholder="Segundo número" class="form-control">
        </div>
        <div class="col-md-3 col-10 mt-md-0 mt-3">
          <select @change="evento => estado.operacao = evento.target.value" class="form-control custom-select">
            <option value="adicao">Adição</option>
            <option value="subtracao">Subtração</option>
            <option value="multiplicacao">Multiplicação</option>
            <option value="divisao">Divisão</option>
          </select>
        </div>
      </div>
    </form>
    <p v-if="(estado.numero1 == '') || (estado.numero2 == '')" class="mt-3">O resultado é igual a</p>
    <p v-else class="mt-3">O resultado é igual a {{ realizaOperacao() }}</p>
    <p class="warning mt-5">* A precisão das operação está restrita a, no máximo, três casas decimais</p>
  </div>
</template>

<style>
  * {
    background-color: #1f0a1d;
    color: #e5ead4;
  }

  .warning{
    color: #a397a3;
    font-size: 12px;
  }

  .custom-select option{
    background-color: #e5ead4;
    color: #1f0a1d;
  }
</style>
