# Inspetora de Periféricos de Placas de Notebook

## Descrição do Sistema

A máquina inspetora tem como objetivo realizar a inspeção automatizada de
periféricos presentes em placas de hardware de notebooks.

O sistema captura placas armazenadas em bandejas, posiciona-as diante de
câmeras de visão computacional e classifica cada placa como **aprovada ou
reprovada**.

A automação da máquina é realizada através de um **CLP**, responsável pelo
controle de motores, sensores e segurança do sistema. A interface de operação e
processamento de visão computacional são executados em **Python**.

---

## Funcionamento Geral

1. O operador posiciona placas de notebook em uma bandeja de entrada.
2. A máquina se desloca até a posição da placa.
3. A garra ajustável captura a placa.
4. A placa é transportada até a posição de inspeção em frente às câmeras.
5. As câmeras realizam a análise dos periféricos via visão computacional.
6. O sistema classifica a placa como **Aprovada** ou **Reprovada**.
7. A placa é depositada em bandejas separadas de saída.

---

## Componentes Principais

### Estrutura Mecânica

- Estrutura em perfis de alumínio
- Painéis de vidro de proteção
- Base de sustentação
- Trilhos lineares
- Bandejas para placas

### Sistema de Movimentação

- Eixo X
- Eixo Y
- Eixo Z

### Sistema de Manipulação

- Garra ajustável para captura das placas

### Sistema de Visão

- 1 câmera de alinhamento e apoio fiducial
- 3 câmeras do fluxo principal de inspeção

### Sistema de Controle

- CLP para controle da automação
- Interface de operação em Python

---

## Situação Atual do Projeto de Software

O sistema já possui uma base funcional para:

- movimentação manual dos eixos X, Y e Z
- comunicação com CLP via Modbus TCP
- gerenciamento de programas de inspeção
- captura de imagens por múltiplas câmeras
- definição de regiões de inspeção
- gerenciamento de bandejas
- definição de regiões de segurança
- controle de ciclo automático
- calibração
- persistência de dados de produção e rastreabilidade

Esta pasta deve ser lida como documentação do estado atual do software e do
domínio, não como redefinição da arquitetura já saneada no repositório.

---

## Câmeras da Inspetora

No estado atual do software, os papéis de câmera são:

- `fiducial`
- `top`
- `bottom`
- `side`

Regras:

- `fiducial` é separada do fluxo principal de inspeção
- `top`, `bottom` e `side` são as câmeras da inspeção principal
- aliases de UI como `Câmera 1`, `Câmera 2` e `Câmera 3` devem ser lidos como
  `top`, `bottom` e `side`

Se houver proposta futura de outro arranjo físico de câmeras, ela deve ser
documentada como evolução futura e não substituir esta descrição do estado
atual.

---

## Navegação da Documentação

- [[../estado_atual_codigo|Estado Atual do Código]]
- [[arquitetura_sistema|Arquitetura do Sistema]]
- [[fluxograma_operacao|Fluxograma de Operação]]
- [[fluxograma_segurança|Fluxograma de Segurança]]
- [[diagrama_estados|Diagrama de Estados da Máquina]]
- [[lógica_clp|Lógica do CLP]]
- [[visão_computacional|Sistema de Visão Computacional]]
- [[lista_sensores|Lista de Sensores]]
- [[lista_atuadores|Lista de Atuadores]]
- [[estrutura_codigo_existente|Estrutura do Código Existente]]
- [[programas_de_inspecao|Programas de Inspeção]]
- [[bandejas_e_regioes_seguranca|Bandejas e Regiões de Segurança]]
- [[calibracao|Calibração]]
- [[persistencia_e_rastreabilidade|Persistência e Rastreabilidade]]
- [[lacunas_para_adaptacao_inspetora|Lacunas para Adaptação da Inspetora]]
