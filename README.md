# Pac-Man AI Agent — Algoritmo Minimax 🕹️🤖

Este repositório contém a implementação de um agente inteligente para o clássico jogo Pac-Man, desenvolvido como projeto prático para a unidade curricular de **Inteligência Artificial**. O objetivo principal é aplicar conceitos de busca adversarial e tomada de decisão num ambiente multiagente complexo.

O agente foi construído utilizando o algoritmo **Minimax**, permitindo que o Pac-Man preveja as ações dos seus adversários (fantasmas) e selecione estrategicamente a melhor jogada possível para maximizar a sua pontuação e garantir a sua sobrevivência.

---

## 🚀 Funcionalidades e Destaques

- **Árvore de Procura Adversarial**: Implementação estruturada através de uma função recursiva que simula cenários futuros de jogo baseados em turnos alternados.
- **Suporte Multiagente Simétrico**: Arquitetura projetada para lidar com múltiplos fantasmas sequenciais. O algoritmo alterna corretamente entre:
  - **Nó MAX (Pac-Man)**: Escolhe a ação que maximiza a utilidade calculada.
  - **Nó MIN (Fantasmas)**: Assume que os oponentes jogarão de forma ótima para minimizar a utilidade do Pac-Man.
- **Função de Avaliação Avançada (`betterEvaluationFunction`)**: Heurística personalizada que calcula dinamicamente o estado do jogo utilizando a **Distância de Manhattan** para mapear:
  - A proximidade das pastilhas de comida restantes.
  - A distância segura em relação aos fantasmas ativos.
  - O estado de vulnerabilidade dos fantasmas (quando assustados pelas cápsulas de poder).
- **Controlo Dinâmico de Profundidade**: Suporte a argumentos em linha de comandos para limitar o nível de antecipação (`depth`), equilibrando inteligência e tempo de processamento.

---

## 📂 Visão Geral da Implementação

O núcleo lógico do projeto reside no ficheiro `seuPacManAgents.py`, estruturado da seguinte forma:

1. **Condição de Paragem (Caso Base)**:
   A cada chamada recursiva, o algoritmo avalia se o estado atual é terminal — vitória (`state.isWin()`), derrota (`state.isLose()`) — ou se o limite predefinido de profundidade foi atingido (`depth == self.depth`). Se sim, a heurística quantifica numericamente a qualidade daquele estado.

2. **Cálculo de Turnos e Agentes**:
   ```python
   numAgents = state.getNumAgents()
   nextAgent = (agentIndex + 1) % numAgents
   nextDepth = depth + 1 if nextAgent == 0 else depth
