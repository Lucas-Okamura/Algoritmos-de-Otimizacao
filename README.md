# Algoritmos de Otimização para Problemas de Produção

Códigos desenvolvidos para a disciplina PRO3515 da Escola Politécnica da USP
para otimizar problemas de produção de modo a diminuir o _makespan_ de 
_jobs_ a serem realizados por um determinado conjunto de máquinas. Isto é,
diminuir tempo de conclusão de todos _jobs_.
Os algoritmos se baseiam principalmente em heurísticas.

Entre os programas, incluem-se os seguintes problemas e algoritmos:

### 1. Máquina Única - Algoritmo de Moore:

* **algoritmo_moore.ipynb**

Em um problema de máquina única, utiliza-se o Algoritmo de Moore para 
diminuir o _makespan_, sendo seu procedimento especificado abaixo:


	* Passo 1: Crie uma lista L1 com todos os jobs e uma lista L2 vazia, que será a 
	lista dos jobs atrasados (backlog list);

	* Passo 2: Ordene L1 pela data de entrega prometida (due date);

	* Passo 3: Se todos os jobs em L1 estiverem dentro do prazo, vá ao passo 5.
	Senão, identifique em L1, entre o primeiro job e o primeiro job atrasado na
	lista, o job que tiver o maior tempo de processamento;

	* Passo 4: Retire o job de maior tempo de processamento do passo anterior,
	inclua-o ao final de L2 e volte ao passo 3.

	* Passo 5: Adicione os jobs de L2 ao final de L1. A lista L1 será uma sequência
	com o menor número de jobs atrasados possível.

### 2. Máquinas Paralelas - LPT e SPT:


* **Desafio 2 - PMP LPT - Dupla 09.ipynb**

Em um problema de máquinas paralelas, os _jobs_ são divididos entre máquinas
que funcionam simultaneamente. Utilizando o método heurístico PMP - LPT
(_Parallel Machine Problem_ - _longest processing time_), tem-se os passos:

	* Passo 1: Ordenar os jobs em ordem decrescente dos tempos de 
	processamento (LPT);

	* Passo 2: Seguindo a ordem LPT, alocar os jobs na máquina com menor 
	carga (soma dos tempos de processamento dos jobs já alocados). Em caso 
	de empate, escolher arbitrariamente uma entre as máquinas com menor 
	carga (p.ex: máquina de menor índice);

	* Passo 3: Definidas as alocações, ordenar os jobs em cada máquina em
	ordem crescente dos tempos (SPT). A esquematização encontrada é aquela
	que minimiza o makespan.

OBS: O código para máquinas paralelas foi desenvolvido para ler arquivos
de extensão .xlsx e adquirir dados a partir dele utilizando a biblioteca _pandas_. O arquivo 
"xl06 3 A PMP Cmax LPT-SPT.xlsx" mostra exemplos de como os dados devem 
ser dispostos na planilha.

### 3. Máquinas em Série - PFSP (_Permutation Flow Shop Problem_):

#### 3.1. Algoritmo de Campbell, Dudek e Smith (CDS)

* **Desafio 3 - CDS - Dupla 09.ipynb**

Foi elaborado o algoritmo heurístico de Campbell, Dudek e Smith (CDS),
que se baseia na aplicação continua do algoritmo de _Johnson_ , de forma 
a minimizar o _makespan_. De modo a simplificar o problema, 
considerou-se que a ordem dos _jobs_ a seremrealizados deveria ser 
a mesma nas duas máquinas disponíveis.

Sua lógica consiste em resolver m-1 problemas F2|prmtu|Cmax, 
com tempos derivados do problema original, usando o algorimto de 
_Johnson_ e comparar o desempenho das m-1 sequências geradas no problema 
original. A melhor dentre as m-1 sequências será considerada a solução 
heurística do problema original.

OBS: O código para máquinas paralelas foi desenvolvido para ler arquivos
de extensão .xlsx e adquirir dados a partir dele utilizando a biblioteca _xlwings_. O arquivo 
"xl05 2 A PFSP Cmax CDS.xlsx" mostra exemplos de como os dados devem 
ser dispostos na planilha.

#### 3.2. Algoritmo de Nawaz, Enscore e Ham (NEH)

* **Desafio 4 - PFSP NEH - Dupla 09.ipynb**

O código roda o algoritmo de NEH, outro método para resolver o problema
de máquinas em série. O algoritmo está explicitado no artigo "A Heuristic 
Algorithm for the m-Machine, n-Job Flow-shop Sequencing Problem", 1983, por 
Nawaz, Muhammad; Jr, E Emory Enscore; Ham, Inyong. Resumidamente, tem-se 
os passos abaixo:

	* Passo 1: Ordenar a lista de jobs em ordem decrescente do tempo total de processamento;

	* Passo 2: Retire os dois primeiros da lista ordenada e crie uma nova lista, teste as duas permutações, escolha a 
	permutação com menor makespan;

	* Passo 3: Retire o próximo job da lista ordenada, teste em todas as posições da nova lista, escolha a inserção
	com menor makespan;

	* Passo 4: Repita o passo 3 até esvaziar a lista ordenada; a nova lista resultante será a solução do problema

OBS: O código para máquinas paralelas foi desenvolvido para ler arquivos
de extensão .xlsx e adquirir dados a partir dele utilizando a biblioteca _xlwings_. O arquivo 
"xl05 2 A PFSP Cmax CDS.xlsx" mostra exemplos de como os dados devem 
ser dispostos na planilha.

#### 3.3. Algoritmo de _Local Search_ (LS)

* **Desafio 5 - PFSP LS - Dupla 09.ipynb**

O algoritmo de _Local Search_ para máquinas em série se baseia na retirada e inserção de
jobs em uma determinada sequência, recalculando o makespan máxima e iterando até encontrar
um valor ótimo, através de uma busca exaustiva. O pseudocódigo para este algoritmo é mostrado abaixo:

```
leia os dados de entrada (solução inicial)
bestCmax=cmax da solução inicial
melhoria=Verdadeiro
enquanto melhoria faça:
   melhoria=Falso
   jotas=lista de indices de 1 a n
   jotas=jotas embaralhados
   para cada j1 em jotas faça:
      remova o job da posição j1 e chame-o de job1
      bestPos=j1
      para j2=1 até n faça:
         insira o job1 na posição j2
         calcule o cmax
         se cmax<bestCmax então:
            bestPos=j2
            melhoria=Verdadeiro
	    bestCmax=cmax
         retire o job1 da posição j2
      insira o job1 na melhor posição
retorna jobs e cmax
```

OBS: O código para máquinas paralelas foi desenvolvido para ler arquivos
de extensão .xlsx e adquirir dados a partir dele utilizando a biblioteca _xlwings_. O arquivo 
"xl10 1 B PFSP Cmax NEH.xlsx" mostra exemplos de como os dados devem 
ser dispostos na planilha.

#### 3.4. Algoritmo de _Iterated Greedy_ (IG)

O Algoritmo de _Iterated Greedy_ é uma meta-heurística, que se trata de uma busca
exaustiva das soluções possíveis até encontrar a melhor. Para o programa desenvolvido,
a solução inicial é aquela encontrada pelos métodos NEH + LS. Detalhes do método podem
ser encontrados no artigo de Ruiz & Stützle, 2007.

* **Desafio 6 - PFSP IG - Dupla 09.ipynb**

OBS: O código para máquinas paralelas foi desenvolvido para ler arquivos
de extensão .xlsx e adquirir dados a partir dele utilizando a biblioteca _xlwings_. O arquivo 
"xl10 2 B PFSP Cmax NEH-LS.xlsx" mostra exemplos de como os dados devem 
ser dispostos na planilha.