
# MetrôBot SP 2.0 (Linhas 1, 2 e 3)

**Integrantes do grupo:**
- Bruna Karlla Fernandes Marques RA: 2025115639
- Dioleno Matias Dos Santos RA: 2893378
- Janaina Maria Abreu da Silva RA: 2780529

Este projeto implementa um MetrôBot para as linhas 1, 2 e 3 do metrô de São Paulo, utilizando uma abordagem de IA neuro-simbólica. Ele combina algoritmos de busca (BFS/DFS), um motor de inferência baseado em regras e um interpretador/narrador de linguagem natural para planejar e descrever rotas de metrô.

## 🎯 A Missão do Projeto

A diretoria do "MetrôBot" gostou do protótipo e quer a versão 2.0: agora cobrindo três linhas do metrô de São Paulo. Linha 1-Azul (Tucuruvi – Jabaquara) Linha 2-Verde (Vila Madalena – Vila Prudente) Linha 3-Vermelha (Palmeiras-Barra Funda – Corinthians-Itaquera) Com várias linhas, a coisa fica muito mais interessante: Existem baldeações (trocar de linha).

## ✨ Implementação e Funcionalidades

Este projeto implementa as seguintes funcionalidades e requisitos:

*   **R1 — Construção do Grafo Multilinhas**: Gera as 52 estações de metrô, garantindo vizinhos únicos e associando cada trecho à(s) linha(s) correspondente(s).
*   **R2 — Algoritmos de Busca (BFS e DFS)**: Implementa Busca em Largura (BFS) e Busca em Profundidade (DFS), ambos respeitando estações bloqueadas. Retornam o caminho encontrado e as estações visitadas para comparação de esforço.
*   **R3 — Base de Conhecimento e Lógica**:
    *   **Locais Conhecidos**: Cadastra 9 locais de interesse (mínimo 3 por linha) para facilitar a busca por pontos turísticos/referência.
    *   **Motor de Inferência (Encadeamento para Frente)**: Utiliza fatos simples e um conjunto de regras (R1-R5 adaptadas) para deduzir novas informações.
    *   **R6 — Integrações Automáticas**: Deduz automaticamente estações de integração (como Sé, Paraíso, Ana Rosa) pela lógica, sem necessidade de entrada manual.
    *   **R7 (Criada pelo Grupo) — Prioridade de Reparo**: Uma regra lógica que identifica estações de integração com elevador em manutenção como prioritárias para reparo.
    *   **Tabela-Verdade**: Demonstração da lógica proposicional `P ∧ (¬Q ∨ R)` aplicada à utilidade de uma estação.
*   **R4 — Interpretação e Narração de Linguagem Natural**:
    *   **Intérprete**: Converte texto livre do usuário em pedidos estruturados (JSON). O LLM *não decide* a rota, apenas interpreta o pedido.
    *   **Narrador**: Descreve a rota calculada pelo algoritmo em linguagem natural, incluindo baldeações.
    *   **Fallback Offline**: Funcionalidade 100% offline (interpretação por regras/palavras-chave e narração por template) caso o LLM não esteja disponível.
*   **R5 — Painel Interativo (`ipywidgets`)**: Uma interface gráfica completa que permite:
    *   Entrada de pedidos em linguagem natural.
    *   Seleção de origem/destino, acessibilidade, estações/linhas bloqueadas, e escolha de algoritmo.
    *   Desenho dinâmico das 3 linhas, destacando a rota, estações visitadas e bloqueadas.
    *   Resumo detalhado da rota (paradas, baldeações, tempo estimado, regras disparadas).
*   **R6 — Testes Automatizados**: Um conjunto robusto de testes (`rodar_testes()`) que valida 10 asserções, incluindo os 6 casos obrigatórios do desafio e casos extras implementados pelo grupo.
*   **Bônus Implementados**:
    *   **Bônus 1 — Menos Baldeações**: Algoritmo que prioriza rotas com menor número de baldeações.
    *   **Bônus 2 — Dijkstra com Tempo Real**: Algoritmo de Dijkstra que considera o tempo de viagem e penalidades por baldeação.
    *   **Bônus 3 — Linha Paralisada (Regra Lógica)**: Utiliza a regra R4 do motor de inferência para automaticamente tornar todas as estações de uma linha paralisada indisponíveis.
    *   **Bônus 4 — Mapa com `networkx`**: Visualização do grafo da rede de metrô utilizando a biblioteca `networkx` para um mapa mais detalhado.
    *   **Bônus 5 — Relatório de Esforço**: Comparação visual do esforço (número de estações visitadas) entre BFS e DFS em várias viagens aleatórias.
*   **Explicação "Para Pensar"**: Uma seção explicativa que aborda por que um determinado cenário de bloqueio (Caso 5 vs. Caso 6) pode ou não resultar em uma rota.

## 🚀 Como rodar o projeto

Para executar este notebook e interagir com o MetrôBot:

1.  **Execute todas as células** do notebook sequencialmente, de cima para baixo. Você pode fazer isso através da opção "Executar tudo" no menu "Ambiente de execução" (Runtime).
2.  O `PROVEDOR` de LLM está definido como "offline" por padrão na célula de configuração (`# ===== Configuração geral =====`). Isso garante que o notebook funcione 100% sem necessidade de internet ou chaves de API, utilizando um interpretador e narrador baseados em regras/templates.
3.  Para usar um LLM real (como Groq ou Ollama), altere a variável `PROVEDOR` para "groq" ou "ollama" na célula de configuração e **configure a chave de API** na variável de ambiente `GROQ_API_KEY` (nunca cole a chave diretamente no código!). Se a chamada da API do LLM falhar por qualquer motivo (ex: sem internet, chave inválida), o código automaticamente retorna para o modo offline.
4.  Após a execução de todas as células, utilize o **painel interativo (`ipywidgets`)** que será renderizado no final do notebook para planejar rotas em linguagem natural ou preenchendo os campos específicos.
5.  A função `rodar_testes()` (localizada na seção `## 🧮 R6 — Testes automatizados`) valida os 6 casos obrigatórios do desafio, além de casos extras implementados pelo grupo, garantindo a correção das implementações.

## 📝 Notas sobre o Desenvolvimento e Uso de IA

### Declaração de uso de IA

Neste desafio, assistentes de IA foram utilizados como ferramentas de apoio para refatoração de código, sugestões de implementação de algoritmos de busca e inferência, e para aprimorar a clareza das explicações e comentários. Toda a saída gerada por IA foi tratada como rascunho, revisada minuciosamente, compreendida e ajustada para garantir a conformidade com as especificações do desafio e a correção lógica. Os testes automatizados foram cruciais para validar cada implementação.

### Migração de Ambiente

Originalmente, o desenvolvimento foi iniciado no VS Code. No entanto, devido a dificuldades com a instalação de componentes não nativos (como bibliotecas para visualização e interação), o projeto foi migrado para o Google Colab, que ofereceu um ambiente mais adequado e sem erros para a execução e demonstração completa do MetrôBot.

# MetrôBot SP 2.0 (Linhas 1, 2 e 3)

**Integrantes do grupo:**
- Bruna Karlla Fernandes Marques RA: 2025115639
- Dioleno Matias Dos Santos RA: 2893378
- Janaina Maria Abreu da Silva RA: 2780529

Este projeto implementa um MetrôBot para as linhas 1, 2 e 3 do metrô de São Paulo, utilizando uma abordagem de IA neuro-simbólica. Ele combina algoritmos de busca (BFS/DFS), um motor de inferência baseado em regras e um interpretador/narrador de linguagem natural para planejar e descrever rotas de metrô.

## 🎯 A Missão do Projeto

A diretoria do "MetrôBot" gostou do protótipo e quer a versão 2.0: agora cobrindo três linhas do metrô de São Paulo. Linha 1-Azul (Tucuruvi – Jabaquara) Linha 2-Verde (Vila Madalena – Vila Prudente) Linha 3-Vermelha (Palmeiras-Barra Funda – Corinthians-Itaquera) Com várias linhas, a coisa fica muito mais interessante: Existem baldeações (trocar de linha).

## ✨ Implementação e Funcionalidades

Este projeto implementa as seguintes funcionalidades e requisitos:

*   **R1 — Construção do Grafo Multilinhas**: Gera as 52 estações de metrô, garantindo vizinhos únicos e associando cada trecho à(s) linha(s) correspondente(s).
*   **R2 — Algoritmos de Busca (BFS e DFS)**: Implementa Busca em Largura (BFS) e Busca em Profundidade (DFS), ambos respeitando estações bloqueadas. Retornam o caminho encontrado e as estações visitadas para comparação de esforço.
*   **R3 — Base de Conhecimento e Lógica**:
    *   **Locais Conhecidos**: Cadastra 9 locais de interesse (mínimo 3 por linha) para facilitar a busca por pontos turísticos/referência.
    *   **Motor de Inferência (Encadeamento para Frente)**: Utiliza fatos simples e um conjunto de regras (R1-R5 adaptadas) para deduzir novas informações.
    *   **R6 — Integrações Automáticas**: Deduz automaticamente estações de integração (como Sé, Paraíso, Ana Rosa) pela lógica, sem necessidade de entrada manual.
    *   **R7 (Criada pelo Grupo) — Prioridade de Reparo**: Uma regra lógica que identifica estações de integração com elevador em manutenção como prioritárias para reparo.
    *   **Tabela-Verdade**: Demonstração da lógica proposicional `P ∧ (¬Q ∨ R)` aplicada à utilidade de uma estação.
*   **R4 — Interpretação e Narração de Linguagem Natural**:
    *   **Intérprete**: Converte texto livre do usuário em pedidos estruturados (JSON). O LLM *não decide* a rota, apenas interpreta o pedido.
    *   **Narrador**: Descreve a rota calculada pelo algoritmo em linguagem natural, incluindo baldeações.
    *   **Fallback Offline**: Funcionalidade 100% offline (interpretação por regras/palavras-chave e narração por template) caso o LLM não esteja disponível.
*   **R5 — Painel Interativo (`ipywidgets`)**: Uma interface gráfica completa que permite:
    *   Entrada de pedidos em linguagem natural.
    *   Seleção de origem/destino, acessibilidade, estações/linhas bloqueadas, e escolha de algoritmo.
    *   Desenho dinâmico das 3 linhas, destacando a rota, estações visitadas e bloqueadas.
    *   Resumo detalhado da rota (paradas, baldeações, tempo estimado, regras disparadas).
*   **R6 — Testes Automatizados**: Um conjunto robusto de testes (`rodar_testes()`) que valida 10 asserções, incluindo os 6 casos obrigatórios do desafio e casos extras implementados pelo grupo.
*   **Bônus Implementados**:
    *   **Bônus 1 — Menos Baldeações**: Algoritmo que prioriza rotas com menor número de baldeações.
    *   **Bônus 2 — Dijkstra com Tempo Real**: Algoritmo de Dijkstra que considera o tempo de viagem e penalidades por baldeação.
    *   **Bônus 3 — Linha Paralisada (Regra Lógica)**: Utiliza a regra R4 do motor de inferência para automaticamente tornar todas as estações de uma linha paralisada indisponíveis.
    *   **Bônus 4 — Mapa com `networkx`**: Visualização do grafo da rede de metrô utilizando a biblioteca `networkx` para um mapa mais detalhado.
    *   **Bônus 5 — Relatório de Esforço**: Comparação visual do esforço (número de estações visitadas) entre BFS e DFS em várias viagens aleatórias.
*   **Explicação "Para Pensar"**: Uma seção explicativa que aborda por que um determinado cenário de bloqueio (Caso 5 vs. Caso 6) pode ou não resultar em uma rota.

## 🚀 Como rodar o projeto

Para executar este notebook e interagir com o MetrôBot:

1.  **Execute todas as células** do notebook sequencialmente, de cima para baixo. Você pode fazer isso através da opção "Executar tudo" no menu "Ambiente de execução" (Runtime).
2.  O `PROVEDOR` de LLM está definido como "offline" por padrão na célula de configuração (`# ===== Configuração geral =====`). Isso garante que o notebook funcione 100% sem necessidade de internet ou chaves de API, utilizando um interpretador e narrador baseados em regras/templates.
3.  Para usar um LLM real (como Groq ou Ollama), altere a variável `PROVEDOR` para "groq" ou "ollama" na célula de configuração e **configure a chave de API** na variável de ambiente `GROQ_API_KEY` (nunca cole a chave diretamente no código!). Se a chamada da API do LLM falhar por qualquer motivo (ex: sem internet, chave inválida), o código automaticamente retorna para o modo offline.
4.  Após a execução de todas as células, utilize o **painel interativo (`ipywidgets`)** que será renderizado no final do notebook para planejar rotas em linguagem natural ou preenchendo os campos específicos.
5.  A função `rodar_testes()` (localizada na seção `## 🧮 R6 — Testes automatizados`) valida os 6 casos obrigatórios do desafio, além de casos extras implementados pelo grupo, garantindo a correção das implementações.

## 📝 Notas sobre o Desenvolvimento e Uso de IA

### Declaração de uso de IA

Neste desafio, assistentes de IA foram utilizados como ferramentas de apoio para refatoração de código, sugestões de implementação de algoritmos de busca e inferência, e para aprimorar a clareza das explicações e comentários. Toda a saída gerada por IA foi tratada como rascunho, revisada minuciosamente, compreendida e ajustada para garantir a conformidade com as especificações do desafio e a correção lógica. Os testes automatizados foram cruciais para validar cada implementação.

### Migração de Ambiente

Originalmente, o desenvolvimento foi iniciado no VS Code. No entanto, devido a dificuldades com a instalação de componentes não nativos (como bibliotecas para visualização e interação), o projeto foi migrado para o Google Colab, que ofereceu um ambiente mais adequado e sem erros para a execução e demonstração completa do MetrôBot.
