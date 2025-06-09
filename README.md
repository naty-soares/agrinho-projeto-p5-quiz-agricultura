let perguntas = [];
let perguntaAtual = 0;
let respostaSelecionada = -1;
let respostaCorreta = false;
let pontuacao = 0;
let esperandoResposta = false;
let tempoDeSoma = 0; // Tempo para somar a pontuação (em frames)
let jogoIniciado = false; // Flag para controlar o início do jogo
let margem = 30; // Margem lateral para opções
let fimDeJogo = false; // Flag para controlar quando o jogo terminou

function setup() {
  createCanvas(600, 400);

  // Definir perguntas do quiz
  perguntas.push({
    pergunta: "Qual é a principal fonte de nutrientes para as plantas?",
    opcoes: ["Água", "Solo", "Luz", "Oxigênio"],
    respostaCerta: 1,
  });

  perguntas.push({
    pergunta: "O que é o cultivo sustentável?",
    opcoes: [
      "Uso excessivo de pesticidas",
      "Rotação de culturas e respeito ao meio ambiente",
      "Uso de monoculturas",
      "Aumento da produtividade a qualquer custo",
    ],
    respostaCerta: 1,
  });

  perguntas.push({
    pergunta: "Qual é a técnica de plantio que preserva o solo?",
    opcoes: [
      "Agricultura convencional",
      "Agricultura de precisão",
      "Agricultura orgânica",
      "Terraceamento",
    ],
    respostaCerta: 3,
  });

  perguntas.push({
    pergunta: "O que é uma monocultura?",
    opcoes: [
      "Cultivo de uma única espécie de planta",
      "Cultivo de várias espécies de plantas",
      "Cultura de solo",
      "Uso de fertilizantes orgânicos",
    ],
    respostaCerta: 0,
  });

  perguntas.push({
    pergunta: "O que é a rotação de culturas?",
    opcoes: [
      "Plantio da mesma cultura ano após ano",
      "Alternância de diferentes culturas no mesmo campo",
      "Uso intensivo de pesticidas",
      "Aumento da irrigação no campo",
    ],
    respostaCerta: 1,
  });

  perguntas.push({
    pergunta: "Quais são os benefícios da agricultura orgânica?",
    opcoes: [
      "Uso de produtos químicos",
      "Preservação da biodiversidade e saúde do solo",
      "Monocultura",
      "Uso de transgênicos",
    ],
    respostaCerta: 1,
  });

  perguntas.push({
    pergunta: "O que é permacultura?",
    opcoes: [
      "Sistema agrícola baseado em monocultura",
      "Sistema de cultivo que imita os ecossistemas naturais",
      "Uso de fertilizantes químicos",
      "Agricultura intensiva",
    ],
    respostaCerta: 1,
  });

  perguntas.push({
    pergunta: "Qual é o impacto da agricultura no meio ambiente?",
    opcoes: [
      "Nenhum impacto",
      "Desmatamento, degradação do solo e poluição da água",
      "Aumento da biodiversidade",
      "Preservação de ecossistemas",
    ],
    respostaCerta: 1,
  });

  // Novas perguntas
  perguntas.push({
    pergunta: "Qual é a principal função das raízes das plantas?",
    opcoes: ["Realizar a fotossíntese", "Absorver água e nutrientes do solo", "Produzir sementes", "Atrair polinizadores"],
    respostaCerta: 1,
  });

  perguntas.push({
    pergunta: "O que é irrigação por gotejamento?",
    opcoes: [
      "Método que usa aspersores para molhar grandes áreas",
      "Método de irrigação onde a água é aplicada diretamente nas raízes das plantas",
      "Irrigação feita por inundação das plantações",
      "Método que utiliza um sistema de chuva artificial",
    ],
    respostaCerta: 1,
  });

  perguntas.push({
    pergunta: "O que são os agrotóxicos?",
    opcoes: [
      "Produtos usados para adubar o solo",
      "Produtos químicos usados para controlar pragas e doenças das plantas",
      "Fertilizantes naturais para as plantas",
      "Produtos usados para melhorar o sabor dos alimentos",
    ],
    respostaCerta: 1,
  });

  perguntas.push({
    pergunta: "Qual é a função da fotossíntese?",
    opcoes: ["Produzir oxigênio", "Transformar luz solar em energia para a planta", "Absorver dióxido de carbono da atmosfera", "Todas as anteriores"],
    respostaCerta: 3,
  });

  perguntas.push({
    pergunta: "O que significa o termo 'agricultura de precisão'?",
    opcoes: [
      "Agricultura onde se usa grande quantidade de pesticidas",
      "Uso de tecnologia para monitorar e otimizar as práticas agrícolas",
      "Agricultura onde se planta tudo manualmente",
      "Agricultura com monocultura",
    ],
    respostaCerta: 1,
  });
}

function draw() {
  if (!jogoIniciado) {
    // Tela inicial com botão Play
    background(0, 153, 0); // Fundo verde, representando o campo

    // Exibir título
    textSize(36);
    fill(255);
    textAlign(CENTER, CENTER);
    text("Quiz sobre Agricultura", width / 2, height / 4);

    // Botão Play
    fill(255, 215, 0); // Cor amarela para o botão
    rect(width / 2 - 75, height / 2 - 25, 150, 50, 10); // Botão
    fill(0);
    textSize(24);
    text("PLAY", width / 2, height / 2); // Texto do botão

    // Adicionar o texto "Feito por Naty" no canto inferior esquerdo
    textSize(14);
    fill(255);
    textAlign(LEFT, BOTTOM);
    text("Feito por Naty", 10, height - 10);
  } else if (!fimDeJogo) {
    // Quiz do jogo
    if (perguntaAtual < perguntas.length) {
      background(240); // Fundo normal para o quiz

      // Exibir título
      textSize(24);
      fill(0);
      textAlign(CENTER, CENTER);
      text("Quiz sobre Agricultura!", width / 2, 40);

      // Exibir a pergunta
      textSize(18);
      textAlign(CENTER, CENTER);
      text(perguntas[perguntaAtual].pergunta, margem, 100, width - margem * 2);

      // Exibir as opções
      for (let i = 0; i < perguntas[perguntaAtual].opcoes.length; i++) {
        fill(255);
        if (respostaSelecionada === i) {
          fill(173, 216, 230); // Cor de fundo para a opção selecionada
        }
        rect(margem, 140 + i * 50, width - margem * 2, 40, 10); // Alinha as opções de forma mais centrada
        fill(0);
        textSize(16);
        textAlign(LEFT, CENTER);
        text(perguntas[perguntaAtual].opcoes[i], margem + 10, 140 + i * 50 + 20); // Ajuste do texto
      }

      // Verificar resposta
      if (respostaSelecionada !== -1 && !esperandoResposta) {
        if (respostaSelecionada === perguntas[perguntaAtual].respostaCerta) {
          respostaCorreta = true;
        } else {
          respostaCorreta = false;
        }

        esperandoResposta = true; // Aguarda antes de avançar
        tempoDeSoma = frameCount + 60; // Adiciona 2 segundos de espera para somar a pontuação
      }

      // Exibir feedback após responder
      if (respostaSelecionada !== -1) {
        textSize(18);
        if (respostaCorreta) {
          fill(0, 255, 0); // Verde para resposta correta
          text("Resposta correta!", width / 2, height - 50);
        } else {
          fill(255, 0, 0); // Vermelho para resposta errada
          text("Resposta errada!", width / 2, height - 50);
        }

        // Exibir pontuação
        textSize(18);
        fill(0);
        text("Pontuação: " + pontuacao, width / 2, height - 30);
      }

      // Quando o tempo de soma for atingido, soma os pontos
      if (esperandoResposta && frameCount > tempoDeSoma) {
        if (respostaCorreta) {
          pontuacao++;
        }
        avancarPergunta(); // Avançar para a próxima pergunta após a soma
      }
    } else {
      // Quando terminar o quiz, vai para a tela de fim de jogo
      fimDeJogo = true;
    }
  } else {
    // Tela de resultado final
    background(255); // Fundo branco

    textSize(24);
    fill(0);
    textAlign(CENTER, CENTER); // Alinha o texto ao centro
    text("Fim de Jogo!", width / 2, height / 2 - 40); // Frase de fim de jogo
    textSize(20);
    text("Sua pontuação final é: " + pontuacao, width / 2, height / 2 + 40); // Exibe a pontuação

    // Instrução para reiniciar o jogo
    textSize(16);
    text("Clique para reiniciar!", width / 2, height / 2 + 80);
  }
}

function mousePressed() {
  if (!jogoIniciado) {
    // Verificar se o clique foi no botão Play
    if (mouseX > width / 2 - 75 && mouseX < width / 2 + 75 && mouseY > height / 2 - 25 && mouseY < height / 2 + 25) {
      jogoIniciado = true; // Começar o jogo
    }
  } else if (fimDeJogo) {
    // Reiniciar o quiz quando clicar na tela após o fim
    resetQuiz();
  } else {
    if (perguntaAtual < perguntas.length) {
      // Verificar qual opção foi clicada
      for (let i = 0; i < perguntas[perguntaAtual].opcoes.length; i++) {
        if (mouseX > margem && mouseX < width - margem && mouseY > 140 + i * 50 && mouseY < 140 + i * 50 + 40) {
          if (!esperandoResposta) { // Só pode selecionar se não estiver esperando
            respostaSelecionada = i;
          }
        }
      }
    }
  }
}

function avancarPergunta() {
  respostaSelecionada = -1; // Resetar a resposta selecionada
  esperandoResposta = false; // Resetar a espera pela resposta

  perguntaAtual++; // Avançar para a próxima pergunta

  // Se o quiz terminar, mostrar uma mensagem final
  if (perguntaAtual >= perguntas.length) {
    fimDeJogo = true; // Sinaliza que o jogo terminou
  }
}

function resetQuiz() {
  perguntaAtual = 0;
  pontuacao = 0;
  respostaSelecionada = -1;
  esperandoResposta = false;
  tempoDeSoma = 0;
  fimDeJogo = false; // Reseta a flag do fim de jogo
  jogoIniciado = false; // Volta para a tela inicial
  loop(); // Reiniciar o loop do jogo
}

