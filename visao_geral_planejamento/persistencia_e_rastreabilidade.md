# Persistência e Rastreabilidade

## Objetivo

Descrever os mecanismos de persistência já existentes no software e sua importância para operação e evolução do sistema.

---

## Tipos de persistência observados

### JSON

Usado para cadastros e parâmetros, como:

- bandejas
- regiões de segurança
- configurações

### Imagens e arquivos de projeto

Usados para:

- referências visuais
- mapas
- ROIs
- capturas

### Bancos SQLite

Arquivos observados:

- `production/production_orders.db`
- `production/program_sync.db`
- `production/traceability.db`

---

## Importância para a Inspetora

A máquina de inspeção não deve apenas mover e inspecionar. Ela também precisa registrar:

- qual programa foi usado
- qual placa foi inspecionada
- qual foi o resultado
- quais imagens foram capturadas
- quando o ciclo ocorreu
- se houve interrupção ou retomada

---

## Funcionalidades já observadas

Também foi identificado suporte a:

- histórico de ciclos
- retomada de ciclo interrompido
- estado salvo de execução
- sincronização de programas
- base para rastreabilidade

---

## Documentos Relacionados

- [[programas_de_inspecao|Programas de Inspeção]]
- [[estrutura_codigo_existente|Estrutura do Código Existente]]
- [[diagrama_estados|Diagrama de Estados]]