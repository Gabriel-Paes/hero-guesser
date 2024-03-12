<template>
  <!-- <HelloWorld /> -->
  <v-container class="fill-height">
    <v-row justify="center">
      <v-col cols="12" style="text-align: center">
        <v-paragraphe> {{ currentQuestion }} </v-paragraphe>
      </v-col>
      <v-col cols="12" style="text-align: center">
        <v-btn @click="sendAnswer(1)" class="mr-4" color="success">Sim</v-btn>
        <v-btn @click="sendAnswer(0)" class="ml-4" color="error">Não</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
//
const perguntas = [
  {
    pergunta: "Seu herói é homem?",
    caracteristica: ["homem"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói é do bem?",
    caracteristica: ["bem"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói Usa Capa?",
    caracteristica: ["capa"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói usa Máscara?",
    caracteristica: ["máscara"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói usa Tecnologia?",
    caracteristica: ["tecnologia"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói usa Armadura?",
    caracteristica: ["armadura"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói é da DC?",
    caracteristica: ["DC"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói é da Marvel?",
    caracteristica: ["Marvel"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói é inteligente?",
    caracteristica: ["inteligente"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói é Rico?",
    caracteristica: ["rico"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói tem poderes?",
    caracteristica: ["poderes"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói voa?",
    caracteristica: ["voar"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói tem super-velocidade?",
    caracteristica: ["super-velocidade"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói tem super força?",
    caracteristica: ["super-força"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói lança teia?",
    caracteristica: ["lança-teia"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói tem um laço da verdade?",
    caracteristica: ["laço-da-verdade"],
    resposta: ["sim", "não"],
  },
  {
    pergunta: "Seu herói tem um 'S' no peito?",
    caracteristica: ["S-no-peito"],
    resposta: ["sim", "não"],
  },
];

export default {
  data: () => {
    questions: perguntas;
  },
  methods: {
    sendAnswer(opcao) {
      if (opcao === 1) {
        console.log("Opção escolhida: Sim");
      } else if (opcao === 0) {
        console.log("Opção escolhida: Não");
      }
      // Você pode adicionar aqui qualquer outra lógica que desejar
    },
  },
};
</script>

<style scoped>
/* Adicione estilos personalizados aqui, se necessário */
</style>
