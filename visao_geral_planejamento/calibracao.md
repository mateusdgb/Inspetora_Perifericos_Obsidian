# Calibração

## Objetivo

Registrar os pontos de calibração já existentes no projeto e sua importância para adaptação da Inspetora de Periféricos.

---

## Funcionalidades de calibração observadas

O projeto já possui diversos módulos de calibração:

- `calibration/cnc_calibration_widget.py`
- `calibration/focus_calibration_dialog.py`
- `calibration/fov_calibration_dialog.py`
- `calibration/unified_focus_calibration_dialog.py`
- `dialogs/gripper_offset_calibration_dialog.py`
- `dialogs/fiducial_setup_dialog.py`

---

## Tipos de calibração identificados

- calibração CNC / movimentação
- calibração de foco
- calibração de campo de visão
- calibração de offset da garra
- configuração de fiducial

---

## Importância para a máquina real

A Inspetora de Periféricos depende fortemente de calibração para:

- alinhar câmera e coordenadas mecânicas
- alinhar garra e placa
- alinhar posição de inspeção e ROI
- garantir repetibilidade

---

## Relação com o projeto existente

O software já foi pensado para um sistema de inspeção com alta dependência de calibração, o que é coerente com a máquina real.

A documentação da Inspetora deve reaproveitar essa base e apenas especificar:

- quais calibrações já funcionam
- quais calibrações ainda precisam ser ajustadas para a máquina física atual
- periodicidade de cada calibração

---

## Documentos Relacionados

- [[visão_computacional|Visão Computacional]]
- [[lógica_clp|Lógica do CLP]]
- [[lacunas_para_adaptacao_inspetora|Lacunas para Adaptação]]