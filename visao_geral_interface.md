# Visão Geral da Interface

## Objetivo

Documentar a interface atual do sistema de inspeção visual da Inspetora de
Periféricos, com foco em:

- navegação
- ações do usuário
- ações do sistema
- organização do estado atual para evolução incremental

Fonte de verdade externa do estado atual:

- [[estado_atual_codigo]]

## Estrutura observada

A interface atual possui como navegação principal:

- menu superior **Configurações**
- menu superior **Calibrações**
- aba **Inspeção**
- aba **Projeto**
- aba **Câmera Fiducial**

## Telas principais observadas

### Inspeção

Tela voltada para execução do processo de inspeção, visualização das câmeras,
carregamento de programa, início/parada de ciclo e decisão final da peça.

### Projeto

Tela voltada para criação e edição de programas de inspeção, captura de
imagens, definição da região da placa, desenho de ROI e configuração de
posições de captura.

### Câmera Fiducial

Tela voltada para movimentação, visualização da câmera fiducial, cadastro e
edição de posições e operação associada ao posicionamento da garra.

## Menus superiores observados

### Configurações

Possui opções ligadas a:

- tema
- simulação
- configuração de câmeras
- conexão CLP
- cadastro de bandejas

### Calibrações

Possui opções ligadas a:

- calibração de entrada
- offset da garra
- CNC
- foco
- FOV
- pontos fiduciais
- velocidades jog

## Papel dessa documentação

Essa documentação deve:

- organizar o conhecimento da navegação
- separar estado atual de backlog futuro
- apontar lacunas reais sem reabrir arquitetura saneada
- servir como base documental para evolução incremental
