# Relatório da NOME DA ATIVIDADE

**Disciplina: PROGRAMAÇÃO CONCORRENTE E DISTRIBUIDA**
**Aluno(s): Maria Eduarda Paim**
**Turma:ADS 4º SEM**
**Professor:Rafael**
**Data:20/03/2026**

---

# 1. Descrição do Problema

Descreva o problema computacional resolvido pelo programa.

O problema consiste no processamento de grandes volumes de arquivos de log contendo informações operacionais. Cada arquivo deve ser analisado para extrair métricas relevantes como número de linhas, palavras, caracteres e contagem de palavras-chave específicas.

Orientações para preenchimento

Foi implementado um sistema de processamento de arquivos de log que realiza:

leitura dos arquivos

contagem de linhas, palavras e caracteres

contagem das palavras-chave: erro, warning e info

O algoritmo utilizado percorre todos os arquivos da pasta e processa cada linha individualmente.

O tamanho da entrada utilizada foi:

1000 arquivos

10.000.000 linhas

200.000.000 palavras

1.366.663.305 caracteres

O objetivo da paralelização foi reduzir o tempo de execução utilizando múltiplos processos.

Objetivo do programa: Processar arquivos de log e extrair estatísticas de forma eficiente

Volume de dados: 1000 arquivos com milhões de linhas

Algoritmo: varredura sequencial por arquivo com contagem de métricas

Complexidade: aproximadamente O(n), onde n é o número total de linhas

---

# 2. Ambiente Experimental

Descreva o ambiente em que os experimentos foram realizados.

## Orientações

Informar as características do hardware e software utilizados na execução dos testes.

| Item                        | Descrição            |
| --------------------------- | ---------            |
| Processador                 |  Intel i5 / Ryzen 5  |
| Número de núcleos           |  2,4,8,12            |
| Memória RAM                 |  8GB / 16GB          |
| Sistema Operacional         |Windows               |
| Linguagem utilizada         | Python        |
| Biblioteca de paralelização | multiprocessing |
| Compilador / Versão         | Python 3.x  |

---

# 3. Metodologia de Testes

Os experimentos foram conduzidos medindo o tempo de execução com a função time.time().

Foi utilizada a pasta log2 contendo 1000 arquivos como entrada.

Configurações testadas

1 processo (serial)

2 processos

4 processos

8 processos

12 processos

Procedimento experimental

Cada configuração foi executada 1 vez

Não foi calculada média (execução única)

Testes realizados em máquina local

Sistema sem controle de carga durante execução
---

# 4. Resultados Experimentais

Preencha a tabela com os **tempos médios de execução** obtidos.

## Orientações

* O tempo deve ser informado em **segundos**
* Utilizar a **média das execuções**

| Nº Threads/Processos | Tempo de Execução (s) |
| -------------------- | --------------------- |
| 1                    | 115.96                |
| 2                    | 48.34                 |
| 4                    | 28.55                 |
| 8                    | 18.23                 |
| 12                   | 16.44                 |

---

# 5. Cálculo de Speedup e Eficiência

## Fórmulas Utilizadas

### Speedup

```
Speedup(p) = T(1) / T(p)
```

Onde:

* **T(1)** = tempo da execução serial
* **T(p)** = tempo com p threads/processos

### Eficiência

```
Eficiência(p) = Speedup(p) / p
```

Onde:

* **p** = número de threads ou processos

---

# 6. Tabela de Resultados

Preencha a tabela abaixo utilizando os tempos medidos.

| Threads/Processos | Tempo (s) | Speedup | Eficiência |
| ----------------- | --------- | ------- | ---------- |
| 1                 | 115.96    | 1.0     | 1.0        |
| 2                 |48.34      | 2.40    | 1.20       |
| 4                 |28.55      | 4.06    | 1.01       |
| 8                 |18.23      | 6.36    |0.79        |
| 12                |16.45      | 7.05    |0.59        |

---

# 7. Gráfico de Tempo de Execução

Construa um gráfico mostrando o **tempo de execução em função do número de threads/processos**.

## Orientações

* Eixo X: número de threads/processos
* Eixo Y: tempo de execução (segundos)

Inserir o gráfico abaixo:

![Gráfico Tempo Execução](graficos/tempo_execucao.png)

---

# 8. Gráfico de Speedup

Construa um gráfico mostrando o **speedup obtido**.

## Orientações

* Eixo X: número de threads/processos
* Eixo Y: speedup
* Incluir também a **linha de speedup ideal (linear)** para comparação

Inserir o gráfico abaixo:

![Gráfico Speedup](graficos/speedup.png)

---

# 9. Gráfico de Eficiência

Construa um gráfico mostrando a **eficiência da paralelização**.

## Orientações

* Eixo X: número de threads/processos
* Eixo Y: eficiência
* Valores entre 0 e 1

Inserir o gráfico abaixo:

![Gráfico Eficiência](graficos/eficiencia.png)

---

# 10. Análise dos Resultados

O speedup obtido foi próximo do ideal até 4 processos. A partir disso, o ganho de desempenho começou a diminuir.

A aplicação apresentou boa escalabilidade inicial, porém com redução de eficiência após 8 processos.

A eficiência começou a cair significativamente a partir de 8 processos, indicando saturação dos recursos da máquina.

É provável que o número de processos tenha ultrapassado o número de núcleos físicos disponíveis, causando competição por CPU.

Houve overhead de paralelização devido a:

criação e gerenciamento de processos

comunicação entre processos

divisão de tarefas

Possíveis causas de perda de desempenho

competição por CPU

overhead do sistema operacional

limitação de memória/cache

custo de gerenciamento do Pool

Além disso, o trecho:

for _ in range(1000):
    pass
---

# 11. Conclusão

O paralelismo trouxe um ganho significativo de desempenho, reduzindo o tempo de execução de aproximadamente 116 segundos para 16 segundos, representando um speedup de cerca de 7x.

O melhor desempenho foi observado com 8 processos, que apresentou o melhor equilíbrio entre tempo e eficiência.

O programa apresentou boa escalabilidade até certo ponto, mas com limitações devido ao hardware e overhead.

Melhorias possíveis

ajustar o número de processos ao número de núcleos

utilizar chunksize no Pool

remover processamento artificial desnecessário

otimizar leitura de arquivos

testar outras estratégias como imap_unordered

---
