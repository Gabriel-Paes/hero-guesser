<template>
  <!-- <HelloWorld /> -->
  <v-container class="fill-height">
    <v-row justify="center">
      <v-col cols="12" style="text-align: center">
        <p>{{ currentQuestion?.pergunta }}</p>
      </v-col>
      <v-col cols="12" style="text-align: center">
        <v-btn @click="startGame(1)" class="mr-4" color="success">Sim</v-btn>
        <v-btn @click="startGame(0)" class="ml-4" color="error">Não</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { superHerois, perguntas } from "@/data";

export default {
  data: () => ({
    questions: perguntas,
    heros: superHerois,
    currentQuestion: null,
    answers: [],
    herosAnswer: {},
    limitAnswers: 6,
  }),
  mounted() {
    this.getPerguntas();
  },
  methods: {
    sendAnswer(opcao) {
      if (opcao === 1) {
        console.log("Opção escolhida: Sim");
      } else if (opcao === 0) {
        console.log("Opção escolhida: Não");
      }
    },
    getRandomIndex(length) {
      return Math.floor(Math.random() * length);
    },

    getPerguntas(caracteristica = null) {
      if (caracteristica === null) {
        console.log("getPerguntas01");
        this.currentQuestion =
          this.questions[this.getRandomIndex(this.questions.length)];
        return;
      }

      const perguntasFiltradas = this.questions.filter((pergunta) =>
        pergunta.caracteristica.includes(caracteristica)
      );

      if (perguntasFiltradas.length === 0) {
        console.log("getPerguntas02");
        this.currentQuestion =
          this.questions[this.getRandomIndex(this.questions.length)];
        return;
      }

      console.log("getPerguntas03");
      this.currentQuestion =
        perguntasFiltradas[this.getRandomIndex(perguntasFiltradas.length)];
      return;
    },
    startGame(resposta) {
      /* const resposta = prompt(`${pergunta.pergunta} / Digite Sim ou Não`);
      const confirmResposta = confirm("Confirmar resposta?");
      if (!confirmResposta) {
        startGame(pergunta);
      } */
      var respostaObj = {
        caracterista: this.currentQuestion.caracteristica[0],
        simNao: resposta,
      };

      console.log("respostaObj", respostaObj);

      this.answers.push(respostaObj);

      console.log("this.answers", this.answers);

      var getHeroisFilter = this.heros.filter(
        (heroi) =>
          heroi.caracteristicas[respostaObj.caracterista] === respostaObj.simNao
      );

      console.log("getHeroisFilter", getHeroisFilter);

      let nextPergunta = this.getPerguntas();

      if (getHeroisFilter.length === 1) {
        this.herosAnswer = getHeroisFilter[0];

        var checkAllCarac = true;
        this.answers.map((_resposta) => {
          if (this.herosAnswer.caracteristicas[_resposta.caracterista] === 0) {
            checkAllCarac = false;
          }
        });

        if (checkAllCarac) {
          console.log("AACCCCHOU", this.herosAnswer);
          return alert("Seu herói é:" + this.herosAnswer.heroi);
        }
      } else if (getHeroisFilter.length > 1) {
        var numRandom = Math.floor(Math.random() * getHeroisFilter.length);
        var getRandomHeroi = getHeroisFilter[numRandom];

        console.log("Mais perguntas", getRandomHeroi);

        var getCaracNotResponse = [];
        for (let _carac in getRandomHeroi.caracteristicas) {
          let carac = getRandomHeroi.caracteristicas[_carac];
          if (carac === 1) {
            if (
              this.answers.filter((resposta) => resposta.caracterista === carac)
                .length === 0
            ) {
              getCaracNotResponse.push(_carac);
            }
          }
        }

        console.log("getCaracNotResponse", getCaracNotResponse);

        var numRandomC = Math.floor(Math.random() * getCaracNotResponse.length);
        nextPergunta = this.getPerguntas(getCaracNotResponse[numRandomC]);
        console.log("carac", getCaracNotResponse[numRandomC]);
        console.log("nextPergunta", nextPergunta);
      }

      if (this.answers.length === this.limitAnswers) {
        var joinCaracteristicas = this.answers.map(
          (resposta) => resposta.caracterista
        );
        console.log("joinCaracteristicas");
        var filteHerois = this.heros.filter((heroi) =>
          joinCaracteristicas.filter(
            (caracteristica) => heroi.caracteristicas[caracteristica] === true
          )
        );
        var selectcRandom = Math.floor(Math.random() * filteHerois.length);
        console.log("filteHerois", JSON.stringify(filteHerois));
        if (filteHerois.length === 0) {
          return alert(
            "Não foi possivel encontrar um herói com essas caracteristicas"
          );
        }
        var heroiRandom = filteHerois[selectcRandom];
        return alert("Seu herói é:" + heroiRandom.heroi);
      }

      return this.startGame(nextPergunta);
    },
  },
};
</script>
