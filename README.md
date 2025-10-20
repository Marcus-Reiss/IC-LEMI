# Repositório de Automação do LEMI

> Repositório destinado à manutenção do conhecimento sobre automação industrial no Laboratório de Escoamentos Multifásicos Industriais da USP de São Carlos.
> 
> Criado em 20/10/2025

---

## Diagrama de Estados

### Teoria

Um pouco da teoria associada aos Diagramas de Estados pode ser acessado [aqui](https://drive.google.com/drive/folders/1K_JtINrELo0-6RyR0VND8tAjkm-flZtJ?usp=sharing).

### Elementos de template para confecção de Diagrama de Estados

Nesse [link](https://www.figma.com/design/sUtT1NiWE6Kaxhr6otfkeP/Elementos-de-template-para-Diagramas-de-Estado?node-id=0-1&t=2iYs1DNGS1sRDzut-1) você encontra um projeto no *Figma* no qual há elementos de template tanto para Diagrama de Estados, quanto para esboço de painéis elétricos.

---

## Programação de CLP

Um pouco da teoria associada à programação de CLP pode ser acessado [aqui](https://drive.google.com/drive/folders/1z-P9JIa5zRTL5xun0JkSCE7rshpo8gXD?usp=sharing).

---

## Instalação - TIA Portal V18 Full

Entre nessa [página](https://plc247.com/download-tia-portal-v18-full-video-installation/) e siga o passo a passo nela descrito.

**Obs.:** no primeiro passo, o arquivo cujo download é requerido pode ser encontrado nesse [link](https://drive.google.com/file/d/13wfrFlOETngnLY-gD2ocSbBvPrI2lzrT/view). Caso alguma senha seja pedida durante a instalação, utilizar `plc247.com` .

## Criação de um novo projeto no TIA Portal V18

### Passo 1 - Criação do arquivo

Selecione *Create new project*, dê um nome ao projeto e clique em *Create*.

### Passo 2 - Configuração do CLP

1. Na tela de *First steps*, clique em *Configure a device*.
2. Em seguida, selecione *Add new device*. Na árvore de dispositivos que aparecer, selecione o modelo do CLP com apenas um clique.

   Para o CLP da bancada de automação do LEMI, selecionar conforme descrito abaixo:
   - **Modelo:** SIMATIC S7-1200, CPU 1214C AC/DC/Rly
   - **Identificação:** 6ES7 214-1BG40-0XB0
   - **Versão:** 4.5

3. Clique no botão *Add*.
  
   Se a janela *PLC security settings* aparecer, desmarque a opção *Protects the PLC ...* e clique em *Finish*.

### Passo 3 - Configuração dos módulos de expansão

1. Selecione o slot na página de *Device view*.
2. No canto direito da tela, na janela de *Hardware catalog*, procure o modelo do módulo de expansão e selecione-o com duplo clique.
   
   Para mudar a versão do hardware, clique com botão direito no desenho do módulo, selecione *Properties* e altere a versão na aba *General*.

   Para o módulos da bancada de automação do LEMI, selecionar conforme decrito abaixo:
   - **Módulo de expansão de entradas/saídas digitais:**
     
      - **Modelo:** SM 1223 DI16/DQ16 x 24VDC
      - **Identificação:** 6ES7 223-1BL32-0XB0
      - **Versão:** 2.0
    
   - **Módulo de expansão de entradas analógicas:**
  
      - **Modelo:** SM 1231 AI8
      - **Identificação:** 6ES7 231-4HF32-0XB0
      - **Versão:** 2.1

**Obs.:** caso não esteja utilizando módulos de expansão, pule para o próximo passo.

### Passo 4 - Conexão com o CLP real

1. Conecte-se ao CLP via cabo Ethernet.
2. Na árvore do projeto, clique com botão direito na guia do dispositivo (abaixo da guia *Devices & networks*) e selecione:
   
   *Download to device* &rarr; *Hardware configuration*
   
   Se uma janela de erro aparecer durante a compilação:

   *Device configuration* &rarr; duplo clique no CLP &rarr; *Protection & Security* &rarr; Selecione *Full access (no protection)*

### Passo 5 - Comece a programar

- Na guia *Program blocks* é onde seu código será desenvolvido.
- Na guia *PLC tags* é onde as entradas e saídas terão seus nomes configurados.
- Para carregar o código no CLP, clique com botão direito na guia do dispositivo e selecione:

  *Download to device* &rarr; *Software (all)*

  Na janela que aparecer, mude a flag para *Stop all*, clique em *Load* e depois em *Finish*.

  **Obs.:** para carregar o código, o CLP deve estar em modo *RUN*. Para alterar o modo do CLP, utilize os pequenos botões na parte superior da interface. Se estiver testando seu código e quiser reiniciar o CLP, jogue ele para *STOP* e depois novamente para *RUN*.

## Exemplo de implementação no TIA Portal V18

Na pasta [Testes-iniciais](https://github.com/Marcus-Reiss/IC-LEMI/tree/main/Testes-iniciais) há um projeto básico no TIA, que resolve o problema descrito na imagem presente nessa mesma pasta.

---

## Projeto do Sistema de Compressores

- Todo o código do projeto se encontra no presente repositório, na pasta [The-compressor-project](https://github.com/Marcus-Reiss/IC-LEMI/tree/main/The-compressor-project).

- Todas as demais informações concernentes ao projeto estão nessa [pasta](https://drive.google.com/drive/folders/1CNuaKfnw3un-AahSKrB-T5drlT_RsD4Z?usp=sharing) do Google Drive.
