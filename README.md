# Bancada MS3DP — Simulador POLI / MCKP

Ferramenta web autocontida para experimentar o **Problema de Otimização de Lotes de Impressão (POLI)** em *print farms*, formalizado como **Problema da Mochila com Escolha Múltipla (MCKP)**. O simulador gera instâncias, executa dois algoritmos exatos — **Programação Dinâmica** e **Branch and Bound** — e reproduz os gráficos do artigo que o acompanha.

> Página única em HTML/CSS/JavaScript, **sem dependências externas**. Roda 100% offline no navegador: basta abrir o arquivo.

---

## O problema, em uma frase

Há `r` peças a imprimir; cada peça admite várias **variantes** de fabricação `(peso, valor)`, e é preciso escolher **exatamente uma variante por peça** para maximizar o valor total sem estourar a capacidade `c` da impressora. É NP-completo (redução do Knapsack 0-1) e equivale ao MCKP.

## Funcionalidades

- **Gerador de instâncias** parametrizável (semente, nº de peças `r`, variantes por peça, capacidade `c`), com viabilidade garantida.
- **Dois algoritmos exatos** implementados em JavaScript:
  - Programação Dinâmica — `O(c · n)`, espaço `O(c)` (duas linhas da tabela).
  - Branch and Bound — poda por cota superior; custo independente de `c`.
- **Verificação automática de correção**: confere que os dois algoritmos retornam o mesmo ótimo em todas as instâncias.
- **Quatro gráficos** no estilo do artigo (eixos log, mesmas cores): custo × `r`, nós explorados e taxa de poda × `r`, custo × `c`, e dispersão do custo do B&B.
- **Teste de estresse da Programação Dinâmica**: aumenta a **capacidade `c`** progressivamente até a *parede de tempo* ou a *parede de memória* (tabela `O(c)`), demonstrando o crescimento linear em `c` e a degradação graciosa. Execução assíncrona — não trava o navegador.
- **Exportação**: PNG de cada gráfico e dos resultados em **CSV** e **JSON**.

## Métrica: operações (padrão) × tempo

- **Operações (determinístico)** — padrão. Conta operações elementares dos algoritmos. Com a **mesma semente, os resultados são idênticos a cada execução** e independentes da máquina. É a métrica recomendada para reproduzir e comparar.
- **Tempo medido (ms)** — mede o tempo de relógio real. Útil para sentir o desempenho na sua máquina, mas **varia entre execuções e entre equipamentos** (não reprodutível).

O teste de estresse sempre usa tempo de relógio, pois seu objetivo é justamente medir o limite prático de recursos.

## Como usar

1. Acesse [GitHub Pages](https://github.com/jaderxnet/simulador-print-farm).
2. Abra o arquivo em qualquer navegador moderno (duplo clique).
3. Ajuste os parâmetros no painel à esquerda.
4. Clique em **Executar testes** para os quatro gráficos, ou em **Rodar teste de estresse (DP)** para o teste de limite.
5. Use os botões **PNG**, **Baixar CSV** e **Baixar JSON** para exportar.

Nenhuma instalação, servidor ou conexão é necessária.

## Parâmetros principais

| Parâmetro | Descrição | Padrão |
|---|---|---|
| Métrica de custo | Operações (determinístico) ou Tempo medido (ms) | Operações |
| Semente | Reprodutibilidade da geração | 42 |
| Variantes por peça | Máximo de variantes por peça | 5 |
| Instâncias por ponto | Repetições em cada ponto dos gráficos | 30 |
| Experimento A | Capacidade fixa; varia `r` (inicial, final, passo) | c=200, r=2..28 |
| Experimento B | Peças fixas; varia `c` (×2 por ponto) | r=10, c=50, 8 pontos |
| Teste de estresse | Peças fixas e orçamento de tempo por passo (ms) | r=20, 1000 ms |


## Licença

[MIT](https://opensource.org/licenses/MIT). 

## Autores

Jáder e Marina — PPGCC UFPI.
