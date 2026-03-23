# Visão Geral da Interface

## Objetivo
Documentar a interface atual do sistema de inspeção visual da Inspetora de Periféricos, com foco em:
- navegação
- ações do usuário
- ações do sistema
- organização futura para geração de código por LLM

## Estrutura observada

A interface atual possui como navegação principal:

- menu superior **Configurações**
- menu superior **Calibrações**
- aba **Inspeção**
- aba **Projeto**
- aba **Câmera Fiducial**

## Telas principais observadas

### Inspeção
Tela voltada para execução do processo de inspeção, visualização das câmeras, carregamento de programa, início/parada de ciclo e decisão final da peça.

### Projeto
Tela voltada para criação e edição de programas de inspeção, captura de imagens, definição da região da placa, desenho de ROI e configuração de posições de captura.

### Câmera Fiducial
Tela voltada para movimentação, visualização da câmera fiducial, cadastro/edição de posições e operação associada ao posicionamento da garra.

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

Essa documentação não deve apenas descrever a interface atual.

Ela também deve:

- organizar o conhecimento da navegação
- separar responsabilidades
- identificar lacunas
- orientar uma futura reimplementação em arquitetura mais limpa
- alimentar uma LLM para geração de código

## Documentos relacionados

- [[interface_navegacao/mapa_telas|Mapa de Telas]]
- [[interface_navegacao/lacunas_interface|Lacunas da Interface]]
- [[interface_navegacao/melhorias_interface|Melhorias da Interface]]