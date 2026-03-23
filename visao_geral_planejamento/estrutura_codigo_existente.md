# Estrutura do Código Existente

## Objetivo

Mapear a estrutura atual do projeto de software já existente para a Inspetora de Periféricos, servindo como referência de estrutura e uso por LLM na futura geração de código.

---

## Visão Geral

O projeto já conta com:

- interface gráfica
- integração com CLP
- integração com múltiplas câmeras
- gerenciamento de programas
- inspeção visual
- controle de ciclo
- persistência de dados
- calibração
- segurança

### Entrada principal

- `inspetor_main.py`

Ponto de entrada da aplicação.

---

### Camada de hardware

- `hardware/plc_controller.py`
- `hardware/plc_driver.py`
- `hardware/camera_manager.py`
- `hardware/simulation_plc_driver.py`

Responsável por PLC, câmeras e simulação.

---

### Orquestração

- `orchestrator/hardware_orchestrator.py`
- `orchestrator/inspection_orchestrator.py`

Responsável por coordenação de subsistemas.

---

### Controllers

- `controllers/machine_cycle_controller.py`
- `controllers/inspection_runtime_controller.py`
- `controllers/inspection_region_controller.py`
- `controllers/component_position_controller.py`
- `controllers/plate_region_controller.py`
- `controllers/barcode_region_controller.py`
- `controllers/blue_reference_controller.py`

---

### Services

- `services/program_manager.py`
- `services/program_sequence_runner.py`
- `services/tray_manager.py`
- `services/safety_validator.py`
- `services/inspection_service.py`
- `services/program_execution_factory.py`
- `services/tray_scan_service.py`

---

### Managers

A pasta `managers/` contém diversos gerenciadores especializados para:

- projeto
- imagens
- inspeção
- posição
- interface
- componentes
- preview
- configuração

---

### Widgets e dialogs

A camada de UI já possui componentes para:

- movimentação
- inspeção
- editor de projeto
- controle de ciclo
- seleção de bandejas
- retomada de ciclo
- calibração
- configuração de PLC
- login

---

### Persistência

Persistência observada em:

- arquivos JSON
- imagens em disco
- bancos SQLite

---

## Conclusão

O projeto existente já constitui uma boa base de software de automação e inspeção. O trabalho de adaptação para a Inspetora de Periféricos deve priorizar:

- parametrização correta da máquina real
- ampliação do modelo para 4 câmeras
- integração da garra real
- alinhamento entre software e layout físico da célula

---

## Documentos Relacionados

- [[arquitetura_sistema|Arquitetura do Sistema]]
- [[programas_de_inspecao|Programas de Inspeção]]
- [[lacunas_para_adaptacao_inspetora|Lacunas para Adaptação]]