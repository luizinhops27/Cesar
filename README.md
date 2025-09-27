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
