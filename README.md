# Aprendizado por Reforço com Q-Learning no FrozenLake

Este projeto implementa aprendizado por reforço para resolver o ambiente FrozenLake do Gymnasium, usando o algoritmo Q-Learning. O FrozenLake é um cenário em formato de grade que representa um lago congelado, onde um agente precisa sair do ponto de partida e chegar até o objetivo sem cair nos buracos espalhados pelo caminho. A ideia prática é que ninguém ensina o caminho certo ao agente, ele descobre sozinho, por tentativa e erro, quais movimentos levam ao objetivo e quais levam ao fracasso, exatamente como alguém aprenderia a atravessar um terreno escorregadio testando cada passo.

## Como funciona

O aprendizado por reforço é diferente dos problemas de classificação e regressão, pois aqui não existe um conjunto de dados rotulado dizendo a resposta certa. No lugar disso existe um agente que age no ambiente, recebe recompensas ou punições conforme o resultado das suas ações e, com o tempo, aprende uma política de comportamento que maximiza a recompensa. No FrozenLake, chegar ao objetivo dá recompensa e cair no buraco encerra o episódio sem prêmio, então o agente é empurrado naturalmente a preferir os caminhos que dão certo.

O algoritmo usado é o Q-Learning, que aprende uma tabela onde cada combinação de estado e ação recebe um valor estimado, o famoso valor Q, que representa o quão boa é aquela ação naquele estado pensando no longo prazo. A cada passo o agente escolhe uma ação, observa o que acontece e atualiza esse valor com base na recompensa recebida e na melhor expectativa do estado seguinte. Repetindo isso por muitos episódios, a tabela vai convergindo e o agente passa a saber, em cada posição da grade, qual movimento tende a levá-lo mais perto do objetivo.

Um ponto central desse tipo de algoritmo é o equilíbrio entre explorar e aproveitar. No começo o agente precisa explorar bastante, tomando ações aleatórias para conhecer o ambiente, pois se ele só repetisse o que já parece bom cedo demais acabaria preso num caminho ruim. Com o tempo, conforme a tabela de valores fica mais confiável, ele passa a aproveitar mais o conhecimento adquirido e a agir de forma mais direta rumo ao objetivo.

## Resultados

Após o treino, o agente aprende a atravessar o lago com sucesso, saindo do ponto inicial e alcançando o objetivo sem cair nos buracos. A execução mostra as viagens do agente pela grade, e nas tentativas finais ele chega ao objetivo de forma consistente, o que confirma que a tabela de valores convergiu para uma política que resolve o ambiente.

## Como rodar

Instale as dependências:

```bash
pip install -r requirements.txt
```

Depois abra o notebook e execute as células em ordem:

```bash
jupyter notebook notebook/frozenlake_qlearning.ipynb
```

## Estrutura do projeto

```
reinforcement-learning-gym/
├── notebook/
│   └── frozenlake_qlearning.ipynb   # treino do agente com Q-Learning
├── requirements.txt
└── .gitignore
```

## Observações e próximos passos

O FrozenLake é um ótimo ponto de partida por ter poucos estados e ações, o que deixa a tabela de valores pequena e fácil de entender. A evolução natural é partir para ambientes maiores, onde manter uma tabela para cada estado deixa de ser viável e passa a fazer sentido usar redes neurais para estimar os valores, o que leva ao Deep Q-Learning. Outra frente interessante é ativar a versão escorregadia do FrozenLake, em que o agente nem sempre vai para onde pretende, tornando o ambiente estocástico e o aprendizado bem mais desafiador.
