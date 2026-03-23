# Programas de Inspeção

## Objetivo

Descrever o conceito de programa de inspeção já existente no software, pois ele é central para o funcionamento da máquina e para geração futura de código por LLM.

---

## Conceito

O sistema já trabalha com a ideia de que cada produto ou modelo inspecionado pode ter um **programa de inspeção**.

Esse programa concentra informações como:

- nome do programa
- câmeras utilizadas
- regiões de interesse
- componentes
- imagens de referência
- parâmetros de similaridade
- configurações de inspeção

---

## Arquivos principais

- `services/program_manager.py`
- `services/program_sequence_runner.py`

---

## Responsabilidades do ProgramManager

O `ProgramManager` já fornece base para:

- criar programas
- validar nomes
- salvar mapas
- salvar regiões de código de barras
- salvar ROIs
- salvar JSONs de inspeção
- manter referência ao programa atual

---

## Estrutura de diretórios observada

O projeto salva programas em estrutura semelhante a:

- `modelos/`
- `modelos/projetos/<nome_do_programa>/...`

Com subpastas por câmera.

---

## Importância para a Inspetora

A Inspetora de Periféricos deve usar esse conceito para representar diferentes modelos de placa ou diferentes layouts de inspeção.

Mesmo que inicialmente exista apenas um tipo de placa, é recomendável manter esse modelo, pois ele facilita:

- expansão futura
- reuso
- configuração sem alterar código
- treinamento de LLM sobre a estrutura do domínio

---

## Necessidades de adaptação

- suportar explicitamente 3 câmeras de inspeção + 1 fiducial para calibração da garra
- revisar nomes de subpastas e papéis de câmera
- definir como cada placa é associada a um programa
- definir quais regiões pertencem a cada câmera
- definir como será salva a referência da câmera inferior e laterais

---

## Documentos Relacionados

- [[visão_computacional|Visão Computacional]]
- [[persistencia_e_rastreabilidade|Persistência e Rastreabilidade]]
- [[lacunas_para_adaptacao_inspetora|Lacunas para Adaptação]]