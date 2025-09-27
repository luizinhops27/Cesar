# Cesar
1)	Soma de variáveis de 32 bits: ;

;Área de dados: 
ORG 1026       →Bits menos significativos de Var1 
DW 458 →Bits menos significativos de Var2;     
ORG 1030    →Bits menos significativos de Var2;     
DW 207 →Bits menos significativos de Var2;     
ORG 1024  →Bits menos significativos de Var2; 
DW 80 →Bits menos significativos de Var2;     
ORG 1028     →Bits menos significativos de Var2; 
   
DW 80 →Bits menos significativos de Var2;     
ORG 0 →Bits menos significativos de Var1;
MOV 1026, R0  → Bits menos significativos da primeira variável; 
ADD 1030, R0  → Soma com bits menos significativos da segunda variável; 
MOV R0, 1034 → Salva resultado da soma (nos bits menos significativos); 
MOV #0, R0     → Zera o registrador R0 (prepara para receber o carry); 
ADC R0            → Soma o carry da soma anterior; 
ADD 1024, R0  → Soma com bits mais significativos da primeira variável; 
ADD 1028, R0  → Soma com bits mais significativos da segunda variável; 
MOV R0, 1032  → Salva o resultado (bits mais significativos); 
HLT                   → Encerra o programa.


2) Mover n posições de memória em bloco  
MOV 1024, R0    →Copia o valor contido no endereço de memória 1024 (4) para o registrador R0; 
MOV 1026, R1    →Copia o valor do endereço 1026 (1030) para o registrador R1; 
MOV 1028, R2    →Copia o valor do endereço 1028 (1040) para o registrador R2; 
CMP R2, R1  →Compara os valores em R2 e R1; 
BGT 5     →Se o resultado da comparação foi "maior que”, o programa desvia;
MOV (R1)+,(R2)+→Copia o dado de [1030] para [1040], fazendo R1 virar 1032 e R2 virar 1042; 
SOB R0,  →Decrementa o valor do registrador R0 em 1. Se o resultado for 
diferente de zero, o programa desvia para a linha/endereço 4; 
HLT     → Finaliza o programa; 
ASL R0  →Multiplica o valor em R0 por 2.
ADD R0, R1 →Soma o valor de R0 (8) com R1 (1030), resultando em 1038, 
fazendo R1 apontar para o final do bloco de origem; 
ADD R0, R2         
→Soma o valor de R0 (8) com R2 (1040), resultando em 1048. 
Fazendo R2 apontar para o final do bloco de destino; 
MOV 1024, R0     →Restaura o valor do contador em R0 para 4; 
MOV -(R1), -(R2) →Primeiro, os valores de R1 e R2 são decrementados. Depois, o 
dado do novo endereço apontado por R1 é copiado para o novo endereço apontado 
por R2.
SOB R0,4 →Esta instrução controla o loop, fazendo-o repetir 4 vezes, 
copiando os dados do fim para o começo; 
HLT →Finaliza o programa; 
ORG 1024 →Instrui o montador a colocar os próximos dados a partir do 
endereço de memória 1024;
DW 4  → Número de posições; 
DW 1030 → Início a ser copiada;
DW 1040 → Inicio do destino; 
ORG 1030 → Declarando valores do início; 
DW 11 →Armazena o valor 11;
DW 22 →Armazena o valor 22; 
DW 33 →Armazena o valor 33; 
DW 44 →Armazena o valor 44; 
ORG 1040 →Muda o ponteiro para o endereço 1040; 
DW 0 →Inicializa o bloco de memória de destino com zeros;
DW 0 →Inicializa o bloco de memória de destino com zeros; 
DW 0 →Inicializa o bloco de memória de destino com zeros; 
DW 0 →Inicializa o bloco de memória de destino com zeros;

3) Pesquisa em Vetores
ORG 1024
DW 8                ; → Tamanho do Vetor; Armazena 8 em 1024;
ORG 1026
DW 1000             ; → Posição inicial do vetor; Armazena 1000 em 1026;
ORG 1000
DW 12               ; → Vetor com seus valores; Armazena o valor do vetor na memória;
DW 17               ; → Armazena o valor do vetor na memória;
DW 23               ; → Armazena o valor do vetor na memória;
DW 15               ; → Armazena o valor do vetor na memória;
DW 8                ; → Armazena o valor do vetor na memória;
DW 27               ; → Armazena o valor do vetor na memória;
DW 26               ; → Armazena o valor do vetor na memória;
DW 37               ; → Armazena o valor do vetor na memória;
ORG 0               ; → Programa começa em 0;
MOV 1024, R0        ; → Tamanho do vetor (em palavras);
MOV 1026, R1        ; → Endereço inicial do vetor;
MOV (R1)+, R2       ; → Inicializa o primeiro elemento como sendo o maior;
MOV R0, R3          ; → Inicializa R3 com o índice ("tamanho") do maior elemento;
DEC R0              ; → Inicializa contador (tamanho - 1);
CMP (R1), R2        ; → Compara um elemento com o maior atual;
BLE 4               ; → Desvia se for menor ou igual;
MOV (R1), R2        ; → Se for maior, atualiza R2;
MOV R0, R3          ; → Salva índice do novo maior valor ("contador atual");
ADD #2, R1          ; → Em qualquer caso, incrementa ponteiro;
SOB R0, 14          ; → Controle do laço;
MOV R2, 1028        ; → Fornece maior valor encontrado;
MOV 1024, R4        ; → Calcula índice do maior valor;
SUB R3, R4          ; → índice = tamanho - contador + 1;
INC R4              ; → índice = mem(1024) - R3 + 1;
MOV R4, 1030        ; → Fornece o índice do maior valor;
HLT                 ; → Finaliza o programa.

Exercícios da Página 11
1)	Faça um programa para determinar a posição de um determinado valor (em ASCII) dentro do de um vetor com as características dadas pelo livro (ou no exercício similar resolvido).

ORG 1028        ;Parametro de busca
DW 101

ORG 1024        ;Tamanho do Vetor
DW 26

ORG 1026        ;Posição inicial do vetor
DW 900

ORG 900         ;Vetor com seus valores
DW 97           ; a
DW 98           ; b
DW 99           ; c
DW 100          ; d
DW 101          ; e
DW 102          ; f
DW 103          ; g
DW 104          ; h
DW 105          ; i
DW 106          ; j
DW 107          ; k
DW 108          ; l
DW 109          ; m
DW 110          ; n
DW 111          ; o
DW 112          ; p
DW 113          ; q
DW 114          ; r
DW 115          ; s
DW 116          ; t
DW 117          ; u
DW 118          ; v
DW 119          ; w
DW 120          ; x
DW 121          ; y
DW 122          ; z|

ORG 0
MOV 1024, R0    ; Tamanho do vetor (em palavras)
MOV 1026, R1    ; Endereço inicial do vetor
MOV 1028, R2    ; Carrega o valor de entrada (valor a ser procurado) em R2
MOV 1030, R3    ; Inicializa o indice de busca em R3 (começa de 0)

LOOP_COMPARA:
CMP (R1), R2    ; Compara o valor no vetor (R1) com o valor de entrada (R2)
BEQ ENCONTROU   ; Se forem iguais, desvia para o rótulo ENCONTROU
ADD #2, R1      ; Avança para o próximo elemento do vetor
INC R3          ; Incrementa o índice de busca
DEC R0          ; Decrementa o contador de elementos restantes
BNE LOOP_COMPARA; Se ainda houver elementos, continua o loop

HLT             ; Se não encontrar o valor, termina o programa (não encontrado)

ENCONTROU:
MOV R0, 1030    ; Se encontrou o valor, move o indice (R3) para a posição de saída
HLT             ; Finaliza o programa 

2)	Faça um programa para inicializar um vetor com valores definidos por constante ou valor em memória.

; --- Área de Dados ---
ORG 1024                ; Aloca os dados a partir do endereço de memória 1024
tamanho: DW 3            ; Tamanho do vetor (3 posições)
endereco: DW 1034       ; Endereço inicial do vetor
valor: DW 74              ; Valor a ser movido para o vetor

; --- Código do Programa ---
ORG 0
MOV tamanho, R1         ; R1 = contador do loop (3)
MOV endereco, R2        ; R2 = ponteiro para o vetor (1034)
MOV valor, R0           ; R0 = o valor a ser movido (74)

LOOP_INICIALIZA:
MOV R0, (R2)+           ; Move o valor de R0 para o endereço de R2 e incrementa R2 para a próxima palavra
DEC R1                  ; Decrementa o contador
BNE LOOP_INICIALIZA     ; Se R1 não for zero, volta para o início do loop
HLT                     ; Finaliza o programa

3)	Manipulação de bits: faça sub-rotinas para identificar posição e isolar (mostrar o valor) com máscara para bits individuais, outra para zerar (clear) ou ligar um bit (set) em uma posição indicada como parâmetro, e finalmente uma para contar o número de bits ligados.

ORG 1024
DW 7                    ; → O número a ser testado

ORG 0
MOV 1024, R0            ; → R0 = o número a ser testado
MOV #0, R1              ; → R1 = o contador de bits (inicia em 0)
MOV #4, R2              ; → R2 = o contador do loop (agora para 4 bits)
MOV #1, R3              ; → R3 = a mascara (inicia em 1)

LOOP_CONTA_BITS:
MOV R0, R4              ; → Cria uma copia do numero em R4
AND R3, R4              ; → R4 = R4 AND mascara. O resultado isola o bit atual
TST R4                  ; → Testa o resultado da operacao AND
BEQ PROXIMO_BIT         ; → Se o resultado for 0, pula o incremento
INC R1                  ; → Se o resultado nao for zero, incrementa o contador

PROXIMO_BIT:
ASL R3                  ; → Desloca a mascara para a esquerda para o proximo bit
DEC R2                  ; → Decrementa o contador do loop
BNE LOOP_CONTA_BITS
HLT                     ; → Finaliza o programa
