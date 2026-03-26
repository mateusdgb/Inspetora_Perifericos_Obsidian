# Estrutura do Código Existente

## Objetivo

Mapear a estrutura atual do projeto de software já existente para a Inspetora
de Periféricos, servindo como referência de estrutura e uso por LLM e por
curadoria documental.

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

### Camada de hardware

- `hardware/camera_manager.py`
- `hardware/plc_controller.py`

Responsável pelos contratos principais de câmera e PLC.

### Orquestração

- `orchestrator/hardware_orchestrator.py`
- `orchestrator/inspection_orchestrator.py`
- `orchestrator/hardware/camera_coordinator.py`
- `orchestrator/hardware/movement_coordinator.py`
- `orchestrator/inspection/program_orchestrator.py`

### Controllers

- `controllers/runtime/inspection_runtime_controller.py`
- `controllers/cycle/machine_cycle_controller.py`
- `controllers/regions/inspection_region_controller.py`
- `controllers/regions/component_position_controller.py`
- `controllers/regions/plate_region_controller.py`
- `controllers/regions/barcode_region_controller.py`
- `controllers/regions/blue_reference_controller.py`

### Services

- `services/program_manager.py`
- `services/inspection_service.py`
- `services/tray_manager.py`
- `services/tray_scan_service.py`

### Managers

A pasta `managers/` contém gerenciadores especializados por domínio:

- aplicação
- câmera
- componente
- display
- inspeção
- movimento
- projeto
- UI

### Widgets e dialogs

A camada de UI possui componentes para:

- movimentação
- inspeção
- editor de projeto
- controle de ciclo
- calibração
- configuração de PLC
- login
- fluxo fiducial

### Persistência

Persistência observada em:

- arquivos JSON
- imagens em disco
- estado local do projeto

---

## Conclusão

O projeto existente já constitui uma boa base de software de automação e
inspeção. O trabalho de evolução deve priorizar:

- parametrização correta da máquina real
- preservação do domínio atual de 4 roles de câmera
- integração da garra real
- alinhamento entre software e layout físico da célula

---

## Documentos Relacionados

- [[../estado_atual_codigo|Estado Atual do Código]]
- [[arquitetura_sistema|Arquitetura do Sistema]]
- [[programas_de_inspecao|Programas de Inspeção]]
- [[lacunas_para_adaptacao_inspetora|Lacunas para Adaptação]]
