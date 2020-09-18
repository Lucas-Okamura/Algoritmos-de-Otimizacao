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
	lista dos jobs atrasados (_backlog list_);

	* Passo 2: Ordene L1 pela data de entrega prometida (_due date_);

	* Passo 3: Se todos os _jobs_ em L1 estiverem dentro do prazo, vá ao passo 5.
	Senão, identifique em L1, entre o primeiro _job_ e o primeiro _job_ atrasado na
	lista, o _job_ que tiver o maior tempo de processamento;

	* Passo 4: Retire o _job_ de maior tempo de processamento do passo anterior,
	inclua-o ao final de L2 e volte ao passo 3.

	* Passo 5: Adicione os _jobs_ de L2 ao final de L1. A lista L1 será uma sequência
	com o menor número de _jobs_ atrasados possível.

### 2. Máquinas Paralelas - LPT e SPT:


* **Desafio 2 - PMP LPT - Dupla 09.ipynb**

Em um problema de máquinas paralelas, os _jobs_ são divididos entre máquinas
que funcionam simultaneamente. Utilizando o método heurístico PMP - LPT
(_Parallel Machine Problem_ - _longest processing time_), tem-se os passos:

	* Passo 1: Ordenar os jobs em ordem decrescente dos tempos de 
	processamento (LPT);

	* Passo 2: Seguindo a ordem LPT, alocar os _jobs_ na máquina com menor 
	carga (soma dos tempos de processamento dos jobs já alocados). Em caso 
	de empate, escolher arbitrariamente uma entre as máquinas com menor 
	carga (p.ex: máquina de menor índice);

	* Passo 3: Definidas as alocações, ordenar os _jobs_ em cada máquina em
	ordem crescente dos tempos (SPT). A esquematização encontrada é aquela
	que minimiza o _makespan_.

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