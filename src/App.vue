<script setup>
import { reactive } from 'vue';

const nome = "Thiago"
const meuObj={
  nome:"Thiago",
  filmeFavorito:"Senhor dos Aneis"
}

function dizOla(nome) {
  return `${nome} diz oi`;
}

const enderecoDaImagem ="https://i0.wp.com/hypando.com.br/wp-content/uploads/2022/07/Imagem-destacada-Trigun-Stampede.jpg?fit=1170%2C780&ssl=1"

const botaoEstaDesabilitado = false

const gostaDeTrigun = true



const estado =reactive({
  contador: 0,
  email:'',
  saldo: 5000,
  transferindo:0,
  nomes:['gian', 'paulo', 'patricia'],
  nomeAInserir: '',

})

function incrementar (){
  estado.contador++;
}

function decrementar (){
  estado.contador--;
}

function alteraEmail(evento){
  estado.email = evento.target.value;
}

function mostraSaldoFuturo() {
  const{saldo, transferindo} = estado;
  return saldo - transferindo;
}

function validaValorTransferencia(){
  const{saldo, transferindo} = estado;
  return saldo >= transferindo;
}

function cadastraNome(){
  if(estado.nomeAInserir.length >=3){
    estado.nomes.push(estado.nomeAInserir)
  }else{
    alert("Digite mais caracteres")
  }
  
}

</script>


<template>
  <h1>{{dizOla("thiago")}}</h1>
  <img v-if="gostaDeTrigun" :src="enderecoDaImagem">
  <button :disabled="botaoEstaDesabilitado">enviar mensagem</button>

  <br/>
<hr/>
{{estado.contador}}
<button @click="incrementar" type="button">+</button>
<button @click="decrementar" type="button">-</button>

<br/>
<hr/>

{{estado.email}}
<input type="email" @keyup="alteraEmail">

<br/>
<hr/>

Saldo: {{ estado.saldo }}<br />
Transferindo:{{ estado.transferindo }}<br />
Saldo depois da transferência: {{mostraSaldoFuturo()}}<br />
<input  :class ="{invalido: !validaValorTransferencia()}" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir "/>
<br/>
<hr/>

<ul>
  <li v-for="nome in estado.nomes">
  {{ nome }}
  </li>
</ul>
<input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
<button @click="cadastraNome" type="button">Cadastrar Nome</button>
</template>





<style scoped>

img{
  max-width: 200px;
}

.invalido{
  outline-color: red;
  border-color:red;
}
</style>
