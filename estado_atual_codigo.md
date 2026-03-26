# Estado Atual do Código

## Objetivo

Esta nota é a referência externa de estado atual do projeto.

Ela deve refletir o que o código realmente executa hoje, sem misturar:

- arquitetura desejada
- backlog futuro
- hipoteses antigas

Quando houver conflito entre esta nota e outras notas do vault, esta nota deve
ser usada para corrigir as demais.

---

## Fonte de verdade

A ordem de precedencia para estado atual e:

1. codigo do repositorio
2. `AGENTS.md`
3. `ARQUITETURA.md`
4. `README.md`
5. Obsidian

---

## Dominio de cameras

O sistema trabalha com exatamente 4 roles:

- `fiducial`
- `top`
- `bottom`
- `side`

Regras:

- `fiducial` possui fluxo proprio e aba propria
- `top`, `bottom` e `side` sao as tres cameras do fluxo principal de inspecao
- `Camera 1`, `Camera 2` e `Camera 3` sao aliases de UI para `top`, `bottom`
  e `side`
- nomes legados devem ser normalizados nas bordas de servico e orquestracao

---

## Fluxo principal consolidado

1. `inspetor_main.py` cria `QApplication`
2. autenticacao opcional via `services/auth_service.py`
3. instancia `CameraInspectionApp`
4. `SettingsManager` carrega configuracoes
5. `CameraFactory` cria os `CameraManager`
6. app monta orchestrators, controllers e tabs
7. loop principal do Qt

Tabs principais:

- `Projeto`
- `Inspecao`
- `Camera Fiducial`

---

## Responsabilidades principais

- persistencia de programas: `services/program_manager.py`
- adaptacao de runtime: `orchestrator/inspection/program_orchestrator.py`
- contrato de camera: `hardware/camera_manager.py`
- contrato de PLC: `hardware/plc_controller.py`
- infraestrutura de PLC ativo: `widgets/hardware_ui/hardware_test_tab.py`

---

## Problemas reais conhecidos

- lista de cameras conectadas nao aparece corretamente no dialogo de
  configuracao
- preview/imagem das cameras nao aparece em algumas telas

---

## Itens ainda nao implementados e que nao sao bug

- automacao completa da garra via PLC
- algoritmo final de visao computacional
- validacao definitiva de E-stop com endereco real do PLC

---

## Regra de sincronizacao documental

Quando o codigo mudar:

1. revisar `ARQUITETURA.md` se houver mudanca estrutural
2. revisar `README.md` se mudar entrada, uso ou estrutura de navegacao
3. revisar esta nota
4. revisar apenas as notas filhas realmente afetadas

---

## Notas relacionadas

- [[visao_geral_interface]]
- [[modelo_eventos_interface]]
- [[mapeamento_ui_para_backend]]
- [[regras_estado_interface]]
- [[visao_geral_planejamento/visão_geral|Visao Geral de Planejamento]]
