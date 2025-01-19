# Instruções para as funções criadas

## Lógica Conjunta

#### *Lógica CONJUNTA*

> **Realiza a lógica conjunta do Diagrama de Estados**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> > 
> > ***Temp:*** real **Pressao** (pressão do tanque separador)
> 
> - Chama as funções [OPERAÇÃO - M1](#opera%C3%A7%C3%A3o---m1), [OPERAÇÃO - M2](#opera%C3%A7%C3%A3o---m2), [OPERAÇÃO - M3](#opera%C3%A7%C3%A3o---m3) e [Obtém pressão](#obt%C3%A9m-press%C3%A3o) 



## Modos de operação no contexto da lógica conjunta

#### *OPERAÇÃO - M1*

> **Realiza a "Operação do modo automático no contexto conjunto"**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> > 
> > ***Temp:*** real **Pressao saida** (pressão na saída do conjunto de compressores)
> 
> - Quando "em operação", chama [M1 - Operação iniciada](#m1---opera%C3%A7%C3%A3o-inicada) e [Obtém pressão de saída](#obt%C3%A9m-press%C3%A3o-de-sa%C3%ADda)
> 
> - Quando "saindo da operação", chama [M1 - Operação finalizada](#m1---opera%C3%A7%C3%A3o-finalizada) e pode chamar [Protocolo de Emergência](#protocolo-de-emerg%C3%AAncia)

#### *OPERAÇÃO - M2*

> **Realiza a "Operação do modo manual no contexto conjunto"**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Quando "em operação", chama [M2 - Operação iniciada](#m2---opera%C3%A7%C3%A3o-inicada)
> 
> - Quando "saindo da operação", chama [M2 - Operação finalizada](#m2---opera%C3%A7%C3%A3o-finalizada) e pode chamar [Protocolo de Emergência](#protocolo-de-emerg%C3%AAncia)

#### *OPERAÇÃO - M3*

> **Realiza a "Operação do modo abastecimento no contexto conjunto"**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Quando "em operação", chama [M3 - Operação iniciada](#m3---opera%C3%A7%C3%A3o-inicada)
> 
> - Quando "saindo da operação", chama [M3 - Operação finalizada](#m3---opera%C3%A7%C3%A3o-finalizada) e pode chamar [Protocolo de Emergência](#protocolo-de-emerg%C3%AAncia)



## Caminhos de operação dos modos

#### *M1 - Operação iniciada*

> **Exerce o caminho "Operação iniciada" do modo M1**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> > 
> > ***Temp:*** bool **Crescente** (output da função Monitora pressão); real **P** (pressão no interior do tanque separador)
> 
> - Chama as funções [Obtém pressão](#obt%C3%A9m-press%C3%A3o), [Monitora pressão](#monitora-press%C3%A3o), [Pressão crescente](#press%C3%A3o-crescente) e [Pressão decrescente](#press%C3%A3o-decrescente)

#### *M1 - Operação finalizada*

> **Exerce o caminho "Operação finalizada" do modo M1**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama as funções [Finaliza operação](#finaliza-opera%C3%A7%C3%A3o) e [Atualiza índices](#atualiza-%C3%ADndices)

#### *M2 - Operação iniciada*

> **Exerce o caminho "Operação iniciada" do modo M2**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama as funções [Aciona válvulas - M1 e M2](#aciona-v%C3%A1lvulas-m1-e-m2) e [Aciona compressores](#aciona-compressores)

#### *M2 - Operação finalizada*

> **Exerce o caminho "Operação finalizada" do modo M2**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Finaliza operação](#finaliza-opera%C3%A7%C3%A3o)

#### *M3 - Operação iniciada*

> **Exerce o caminho "Operação iniciada" do modo M3**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> > 
> > ***Temp:*** real **Media** (média dos valores da pressão de abastecimento); real **Threshold de Peq** (é o valor (1 - gamma)*Peq )
> 
> - Chama as funções [Aciona válvulas - M3](#aciona-v%C3%A1lvulas-m3), [Atinge pressão de eq](#atinge-press%C3%A3o-de-eq), [Calcula média - M3](#calcula-m%C3%A9dia---m3), [Aciona compressores](#aciona-compressores), [Atinge Plim](#atinge-plim) e [Finaliza operação - M3](#finaliza-opera%C3%A7%C3%A3o-m3)

#### *M3 - Operação finalizada*

> **Exerce o caminho "Operação finalizada" do modo M3**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Finaliza operação - M3](#finaliza-opera%C3%A7%C3%A3o-m3)



## Modo 1 - funções principais

#### *Monitora pressão*

> **Cerne do modo M1: verifica se a pressão é crescente ou decrescente**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** bool **Crescente** (indica se a pressão é crescente)
> > 
> > ***Temp:*** real **Pressao** (pressão do tanque separador); bool **Positivo 1** (*output* da função *Calcula derivada*); bool **Positivo 2** (*output* da função *Calcula média móvel*)
> 
> - Chama as funções [Obtém pressão](#obt%C3%A9m-press%C3%A3o), [Calcula derivada](#calcula-derivada) e [Calcula média móvel](#calcula-m%C3%A9dia-m%C3%B3vel)
> 
> - Utiliza um **TON** (Timer de amostragem)
> 
> - A pressão é considerada crescente quando **Positivo 1** <u>E</u> **Positivo 2** são *true*
> 
> - A pressão é considerada decrescente quando **Positivo 1** <u>E</u> **Positivo 2** são *false

#### *Pressão crescente*

> **Avalia os casos nos quais a pressão é crescente**
> 
> > ***Input:*** real **P** (pressão no tanque separador)
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Aciona compressores](#aciona-compressores) com **nc** dependente do caso
> 
> - Pode chamar a função [Verifica válvulas 1](#verifica-v%C3%A1lvulas-1)

#### *Pressão decrescente*

> **Avalia os casos nos quais a pressão é decrescente**
> 
> > ***Input:*** real **P** (pressão no tanque separador)
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Desliga compressores](#desliga-compressores)
> 
> - Pode chamar a função [Verifica válvulas 2](#verifica-v%C3%A1lvulas-2) e a [Atualiza índices](#atualiza-%C3%ADndices)



## Modo 3 - funções principais

#### *Atinge pressão de eq*

> **Realiza o que é mostrado em "Atingindo a pressão de equilíbrio na linha direta" no Diagrama de Estados**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> > 
> > ***Temp:*** real **Threshold de Ta** (é o valor (1 - beta)*Ta ); real **Temperatura** (temperatura dada pelo transmissor no nó estendido)
> 
> - Chama a função [Obtém temperatura](#obt%C3%A9m-temperatura)
> 
> - Se **VD2** == *true* chama as funções [Atualiza threshold de Ta](#atualiza-threshold-de-ta) e [Guarda valores de P](#guarda-valores-de-p)

#### *Atinge Plim*

> **Verifica se a pressão da linha de abastecimento atingiu o valor mínimo (Plim)**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Obtém pressão - M3](#obt%C3%A9m-press%C3%A3o---m3)
> 
> - Se **PA** <= **Plim** coloca a variável global **Plim atingida** em *true*



## Funções de finalização e emergência

#### *Finaliza operação*

> **Exerce o estado "Finalizando operação" dos modos M1 e M2**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama as funções [Verifica válvulas 2](#verifica-v%C3%A1lvulas-2) e [Verifica compressores](#verifica-compressores)

#### *Finaliza operação - M3*

> **Exerce o estado "Finalizando operação" do modo M3**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama as funções [Verifica válvulas 2](#verifica-v%C3%A1lvulas-2), [Verifica válvulas 3](#verifica-v%C3%A1lvulas-3) e [Verifica compressores](#verifica-compressores)

#### *Protocolo de Emergência*

> **Realiza o "Protocolo de Emergência" do Diagrama de Estados**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum



## Funções de acionamento

#### *Aciona compressores*

> **Aciona um determinado número de compressores**
> 
> > ***Input:*** int **nc** (número de compressores a serem acionados)
> > 
> > ***Output:*** nenhum
> 
> - Decide qual compressor acionar com base no **nc** e na função [Relaciona índices](#relaciona-índices) com **valor logico** *true* 
> 
> - Altera o valor da variável global **n** 

#### *Aciona válvulas - M1 e M2*

> **Aciona as válvulas on/off  VC e VT**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Coloca a variável global **Valvulas ON** em *true* 

#### *Aciona válvulas - M3*

> **Aciona as válvulas on/off  VD1 e VD2**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Coloca a variável global **Valvulas ON - M3** em *true*



## Funções de desligamento

#### *Desliga compressores*

> **Desliga um determinado número de compressores**
> 
> > ***Input:*** int **nc** (número de compressores a serem desligados)
> > 
> > ***Output:*** nenhum
> 
> - Decide qual compressor desligar com base no **nc** e na função [Relaciona índices](#relaciona-%C3%ADndices) com **valor logico** *false*
> 
> - Altera o valor da variável global **n**

#### *Desliga válvulas - M1 e M2*

> **Desliga as válvulas on/off VC e VT**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Coloca a variável global **Valvulas ON** em *false*

#### *Desliga válvulas - M3*

> **Aciona as válvulas on/off VD1 e VD2**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Coloca a variável global **Valvulas ON - M3** em *false*

  

## Funções que envolvem cálculos

#### *Calcula derivada*

> **Calcula a derivada dos valores de pressão e verifica se ela é positiva**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** bool **Positivo** (recebe *true* se a derivada é positiva)
> > 
> > ***Temp:*** real **Derivada** (derivada dos valores de pressão)

#### *Calcula média móvel*

> **Calcula médias móveis de 5 e 10 valores de pressão e verifica se a pressão é crescente**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** bool **Positivo** (recebe *true* se a média de 10 é maior que a média de 5)
> > 
> > ***Temp:*** int **index 5**, int **index 10** (índices que percorrem o array de valores de pressão); real **soma 5**, real **soma 10** (variáveis auxiliares para o cálculo das médias); real **media 5**, real **media 10** (médias de 5 e 10 valores)
> 
> - Realizada com linguagem SCL

#### *Calcula média - M3*

> **Calcula a média dos valores da pressão de abastecimento**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** real **Media** (média dos valores de pressão)
> > 
> > ***Temp:*** int **index** (índice utilizado no *for loop*); real **soma** (variável auxiliar no cálculo da média)
> 
> - Realizada com linguagem SCL

#### *Guarda valores de P*

> **Armazena os valores da pressão de abastecimento enquanto a VD2 está acionada, no contexto do estado "Atingindo a pressão de equilíbrio na linha direta"**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> > 
> > ***Temp:*** real **Pressao abastecimento** (pressão no nó estendido)
> 
> - Chama a função [Obtém pressão - M3](#obt%C3%A9m-press%C3%A3o---m3)
> 
> - Utiliza um **TON** (Timer abastecimento)

#### *Atualiza threshold de Ta*



## Funções que gerenciam a sequência de índices

#### *Atualiza índices*

> **Altera a sequência de compressores**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Altera o array global **Sequencia[]**  

#### *Relaciona índices*

> **Relaciona a sequência de índices com as saídas do CLP correspondentes aos compressores C1, C2 e C3**
> 
> > ***Input:*** int **index** (índice da sequência de compressores); bool **valor logico** (determina se é preciso acionar ou desligar o compressor)
> > 
> > ***Output:*** nenhum



## Funções de verificação

#### *Verifica compressores*

> **Desliga os compressores que estejam, por ventura, acionados**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Desliga compressores](#desliga-compressores) com **nc** igual a 3

#### *Verifica válvulas 1*

> **Aciona as válvulas do modo recuperação que estejam, por ventura, desligadas**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Aciona válvulas - M1 e M2](#aciona-v%C3%A1lvulas---m1-e-m2)

#### *Verifica válvulas 2*

> **Desliga as válvulas do modo recuperação que estejam, por ventura, acionadas**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Desliga válvulas - M1 e M2](#desliga-v%C3%A1lvulas---m1-e-m2)

#### *Verifica válvulas 3*

> **Desliga as válvulas do modo abastecimento que estejam, por ventura, acionadas**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** nenhum
> 
> - Chama a função [Desliga válvulas - M3](#desliga-v%C3%A1lvulas---m3)



## Funções de leitura de entradas analógicas

#### *Obtém pressão*

> **Realiza o tratamento do sinal de pressão do transmissor para obter a pressão do tanque separador**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** real **Pressao** (pressão do tanque separador)
> > 
> > ***Temp:*** real **Pressao normalizada** (valor normalizado da pressão)
> 
> - Utiliza os blocos **NORM_X** e **SCALE_X**

#### *Obtém pressão - M3*

> **Realiza o tratamento do sinal de pressão do transmissor para obter a pressão no nó estendido**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** real **Pressao abastecimento** (pressão no nó estendido)
> > 
> > ***Temp:*** real **Pressao normalizada** (valor normalizado da pressão)
> 
> - Utiliza os blocos **NORM_X** e **SCALE_X**

#### *Obtém pressão de saída*

> **Realiza o tratamento do sinal de pressão do transmissor para obter a pressão na saída do conjunto de compressores**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** real **Pressao saida** (pressão na saída do conjunto de compressores)
> > 
> > ***Temp:*** real **Pressao normalizada** (valor normalizado da pressão)
> 
> - Utiliza os blocos **NORM_X** e **SCALE_X**

#### *Obtém temperatura*

> **Realiza o tratamento do sinal de temperatura do transmissor para obter a temperatura no nó estendido**
> 
> > ***Input:*** nenhum
> > 
> > ***Output:*** real **Temperatura** (temperatura no nó estendido)
> > 
> > ***Temp:*** real **Temperatura normalizada** (valor normalizado da temperatura)
> 
> - Utiliza os blocos **NORM_X** e **SCALE_X**

### 

### 





### 
