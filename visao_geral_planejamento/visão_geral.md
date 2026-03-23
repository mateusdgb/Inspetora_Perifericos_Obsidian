# Inspetora de Periféricos de Placas de Notebook

## Descrição do Sistema

A máquina inspetora tem como objetivo realizar a inspeção automatizada de periféricos presentes em placas de hardware de notebooks.

O sistema captura placas armazenadas em bandejas, posiciona-as diante de câmeras de visão computacional e classifica cada placa como **aprovada ou reprovada**.

A automação da máquina é realizada através de um **CLP**, responsável pelo controle de motores, sensores e segurança do sistema. A interface de operação e processamento de visão computacional são executados em **Python**.

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

- Eixo X (horizontal)
- Eixo Y (longitudinal)
- Eixo Z (vertical)

### Sistema de Manipulação

- Garra ajustável para captura das placas

### Sistema de Visão

- 1 câmera para alinhamento da garra (fiducial)
- 3 câmeras para inspeção de periféricos

### Sistema de Controle

- CLP para controle da automação
- Interface de operação em Python

---

## Objetivo da Inspeção

Verificar se os periféricos presentes nas placas de notebook estão:

- presentes
- posicionados corretamente
- montados corretamente

Caso algum erro seja identificado, a placa é classificada como **reprovada**.

---

## Situação Atual do Projeto de Software

O sistema da Inspetora de Periféricos já possui uma base de software previamente desenvolvida e adaptada de um projeto similar.

Essa base já inclui funcionalidades implementadas ou parcialmente implementadas para:

- movimentação manual dos eixos X, Y e Z
- comunicação com CLP via Modbus TCP
- gerenciamento de programas de inspeção
- captura de imagens por múltiplas câmeras
- definição de regiões de inspeção
- gerenciamento de bandejas
- definição de regiões de segurança
- controle de ciclo automático
- retomada de ciclo interrompido
- calibração
- persistência de dados de produção e rastreabilidade

A documentação desta pasta deve ser entendida como uma combinação de:

- visão conceitual da máquina
- visão do software já existente
- visão das adaptações necessárias para o caso específico da Inspetora de Periféricos

---

## Câmeras da Inspetora

Na configuração desejada da máquina, existem:

- 1 câmera para posicionamento da garra e leitura de fiducial
- 3 câmeras para inspeção de componentes:
  - 1 câmera inferior
  - 2 câmeras laterais

No projeto atual do software, os papéis de câmera observados são:

- `fiducial`
- `top`
- `bottom`
- `side`

Portanto, será necessária adaptação do modelo atual para suportar explicitamente duas câmeras laterais de inspeção.

---

## Navegação da Documentação

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

---

## Relação entre os Módulos

A operação da máquina depende da integração entre [[lógica_clp]], [[visão_computacional]] e [[arquitetura_sistema]].

O comportamento operacional detalhado está em [[fluxograma_operacao]], enquanto as restrições de proteção estão em [[fluxograma_segurança]].

A definição física dos elementos de entrada e saída está em [[lista_sensores]] e [[lista_atuadores]].