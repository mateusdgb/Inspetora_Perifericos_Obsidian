# Mapeamento UI para Backend

## Objetivo

Este documento relaciona elementos da interface da Inspetora de Periféricos com as camadas internas do sistema.

Ele serve para:

- entender o acoplamento atual entre UI e backend
- orientar uma arquitetura futura mais organizada
- alimentar LLM para geração de código com separação de responsabilidades

Fonte de verdade externa do estado atual:

- [[estado_atual_codigo]]

---

## Estrutura do mapeamento

Cada item deve relacionar:

- **Tela / Componente**
- **Evento**
- **Controller provável**
- **Service / Manager provável**
- **Hardware / Visão / Persistência**
- **Saída esperada**

---

## Tela Projeto

### PROJ-MAP-01 — Novo Programa

**Tela / Componente:** Tela Projeto → botão `Novo Programa`  
**Evento:** clique

**Controller provável:**
- controller de projeto
- controller/editor de programa

**Service / Manager provável:**
- `ProgramManager`
- manager de projeto

**Persistência:**
- diretórios do programa
- JSONs do projeto
- estrutura inicial por role de câmera

**Saída esperada:**
- contexto do programa criado e carregado na tela

---

### PROJ-MAP-02 — Carregar Programa

**Tela / Componente:** Tela Projeto → botão `Carregar Programa`  
**Evento:** clique

**Controller provável:**
- controller de projeto

**Service / Manager provável:**
- `ProgramManager`
- managers de imagem/região/projeto

**Persistência:**
- leitura de dados do programa salvo

**Saída esperada:**
- restauração do contexto do programa

---

### PROJ-MAP-03 — Salvar Alterações

**Tela / Componente:** Tela Projeto → botão `Salvar Alterações`  
**Evento:** clique

**Controller provável:**
- controller de projeto

**Service / Manager provável:**
- `ProgramManager`
- manager de ROIs
- manager de imagens
- manager de posições

**Persistência:**
- escrita de imagens, ROIs, metadados, parâmetros

**Saída esperada:**
- confirmação de salvamento

---

### PROJ-MAP-04 — Capturar Imagem

**Tela / Componente:** Tela Projeto → botão `Capturar Imagem`  
**Evento:** clique

**Controller provável:**
- inspection runtime controller
- controller de captura/projeto

**Service / Manager provável:**
- `CameraManager`
- manager de imagem

**Hardware / Visão:**
- câmera ativa

**Persistência:**
- imagem em buffer ou persistida no projeto

**Saída esperada:**
- imagem exibida e pronta para anotação

---

### PROJ-MAP-05 — Definir Região da Placa

**Tela / Componente:** Tela Projeto → botão `Definir Região da Placa`  
**Evento:** clique

**Controller provável:**
- `plate_region_controller`

**Service / Manager provável:**
- manager de projeto/regiões

**Persistência:**
- metadados da região da placa

**Saída esperada:**
- região desenhada e salva no contexto

---

### PROJ-MAP-06 — Desenhar ROI

**Tela / Componente:** Tela Projeto → botão `Desenhar ROI (+)`  
**Evento:** clique

**Controller provável:**
- `inspection_region_controller`
- `component_position_controller`

**Service / Manager provável:**
- manager de ROIs/componentes

**Persistência:**
- lista de ROIs e metadados

**Saída esperada:**
- ROI criada e associada ao item de inspeção

---

### PROJ-MAP-07 — Subaba Inspeção na Tela Projeto

**Tela / Componente:** Tela Projeto → subaba `Inspeção`  
**Evento:** troca de aba / edição de parâmetros

**Controller provável:**
- `InspectionRegionController`
- `BlueReferenceController`

**Service / Manager provável:**
- `ProgramManager`
- `inspection_service`
- managers de inspeção/projeto da tela ativa

**Persistência:**
- parâmetros de threshold
- % mínimo
- similaridade
- janelas/configurações de inspeção

**Saída esperada:**
- parâmetros refletidos no programa atual e utilizados na inspeção futura

---

### PROJ-MAP-08 — Controles de Movimentação

**Tela / Componente:** painéis de movimento  
**Evento:** clique nos comandos de eixo/garra/home

**Controller provável:**
- controller de movimento/hardware

**Service / Manager provável:**
- orchestrator de hardware
- manager de posição

**Hardware:**
- `PLCController`
- `PLCDriver`
- modo simulado

**Validação:**
- `safety_validator`

**Saída esperada:**
- atualização de posição
- deslocamento físico ou simulado

---
### PROJ-MAP-09 — Programação Rápida / Configuração de Inspeção

**Tela / Componente:** Tela Projeto → subaba `Inspeção` → botões de configuração  
**Evento:** clique em `Programação Rápida`, `Definir Janela Azul`, `Adicionar Inspeção`, `Aplicar Config`, `Aplicar Similaridade`

**Controller provável:**
- inspection configuration controller
- `inspection_region_controller`
- `blue_reference_controller` em parte do fluxo

**Service / Manager provável:**
- `inspection_service`
- managers de inspeção da tela Projeto
- persistência do programa atual

**Persistência:**
- parâmetros de inspeção no programa atual

**Saída esperada:**
- regras de inspeção configuradas para a câmera ou item atual

## Tela Inspeção

### INSP-MAP-01 — Carregar

**Tela / Componente:** Tela Inspeção → botão `Carregar`  
**Evento:** clique

**Controller provável:**
- `machine_cycle_controller`
- `inspection_runtime_controller`

**Service / Manager provável:**
- `ProgramManager`
- inspection manager

**Persistência:**
- leitura do programa/contexto

**Saída esperada:**
- contexto de inspeção carregado

---

### INSP-MAP-02 — Iniciar Ciclo

**Tela / Componente:** Tela Inspeção → botão `Iniciar Ciclo`  
**Evento:** clique

**Controller provável:**
- `machine_cycle_controller`

**Service / Manager provável:**
- `program_sequence_runner`
- `inspection_service`

**Hardware / Visão:**
- PLC
- câmeras
- garra

**Persistência:**
- início de rastreabilidade/ciclo
- eventual estado salvo do ciclo

**Saída esperada:**
- ciclo iniciado e UI atualizada

---

### INSP-MAP-03 — Parar

**Tela / Componente:** Tela Inspeção → botão `Parar`  
**Evento:** clique

**Controller provável:**
- `machine_cycle_controller`

**Service / Manager provável:**
- manager de ciclo

**Hardware:**
- PLC

**Persistência:**
- possível registro de interrupção

**Saída esperada:**
- ciclo parado com segurança

---

### INSP-MAP-04 — Inspecionar

**Tela / Componente:** Tela Inspeção → botão `Inspecionar`  
**Evento:** clique

**Controller provável:**
- `inspection_runtime_controller`

**Service / Manager provável:**
- `inspection_service`
- `peripheral_comparator`

**Hardware / Visão:**
- câmeras
- processamento de imagem

**Persistência:**
- resultado parcial/final
- imagens e falhas quando aplicável

**Saída esperada:**
- falhas e decisão preliminar exibidas

---

### INSP-MAP-05 — Aprovar / Reprovar Peça

**Tela / Componente:** Tela Inspeção → botões `Aprovar Peça`, `Reprovar Peça`  
**Evento:** clique

**Controller provável:**
- controller de inspeção/ciclo

**Service / Manager provável:**
- manager de produção/rastreabilidade

**Persistência:**
- `traceability`
- resultados de produção

**Saída esperada:**
- atualização de contadores e histórico

---

## Tela Câmera Fiducial

### FID-MAP-01 — Ligar câmera fiducial

**Tela / Componente:** Tela Câmera Fiducial → botão `Ligar`  
**Evento:** clique

**Controller provável:**
- controller da câmera fiducial

**Service / Manager provável:**
- `CameraManager`

**Hardware:**
- câmera fiducial

**Saída esperada:**
- preview ativo e status atualizado

---

### FID-MAP-02 — Posições da fiducial

**Tela / Componente:** botões de posição  
**Evento:** adicionar, inserir, editar, remover

**Controller provável:**
- controller de posições
- controller fiducial

**Service / Manager provável:**
- manager de posições/programa

**Persistência:**
- programa fiducial

**Saída esperada:**
- lista de posições atualizada

---

### FID-MAP-03 — Executar programa fiducial

**Tela / Componente:** botão `Executar`  
**Evento:** clique

**Controller provável:**
- controller de execução fiducial

**Service / Manager provável:**
- sequence/program runner
- manager de posições

**Hardware:**
- PLC
- câmera fiducial

**Saída esperada:**
- sequência executada e UI atualizada

---


## Menu Configurações

### CONF-MAP-01 — Tema

**Tela / Componente:** Menu Configurações → `Tema`  
**Evento:** seleção de Auto/Claro/Escuro

**Controller provável:**
- settings/theme controller

**Service / Manager provável:**
- settings manager

**Persistência:**
- preferência visual local

**Saída esperada:**
- tema aplicado na interface

---

### CONF-MAP-02 — Configuração de Simulação

**Tela / Componente:** Menu Configurações → `Simulação`  
**Evento:** clique / salvar

**Controller provável:**
- controller de simulação/configuração

**Service / Manager provável:**
- settings manager
- hardware orchestration
- simulation manager/driver

**Persistência:**
- configuração de modo simulado
- multiplicador e opções de simulação

**Saída esperada:**
- sistema opera em modo real ou simulado

---

### CONF-MAP-03 — Configuração de Câmeras

**Tela / Componente:** Menu Configurações → `Configurar Câmeras...`  
**Evento:** clique e ações internas

**Controller provável:**
- controller de câmeras/configuração

**Service / Manager provável:**
- camera manager
- settings manager

**Hardware / Visão:**
- dispositivos de câmera
- stream/preview

**Persistência:**
- papel lógico das câmeras
- parâmetros de imagem

**Saída esperada:**
- câmeras configuradas e mapeadas ao sistema

---

### CONF-MAP-04 — Configuração CLP

**Tela / Componente:** Menu Configurações → `Conexão CLP...`  
**Evento:** clique e ações internas

**Controller provável:**
- controller de conexão CLP

**Service / Manager provável:**
- PLC controller/driver
- hardware orchestration
- settings manager

**Persistência:**
- IP, porta, timeout, auto-connect
- logs exportáveis

**Saída esperada:**
- comunicação com CLP pronta para uso

---

### CONF-MAP-05 — Cadastro de Bandejas

**Tela / Componente:** Menu Configurações → `Cadastro de Bandejas...`  
**Evento:** clique e ações internas

**Controller provável:**
- controller de cadastro de bandejas

**Service / Manager provável:**
- `tray_manager`
- manager de posição
- manager de fiduciais, quando aplicável

**Hardware / Visão:**
- leitura de posição atual
- eventualmente integração com fiduciais

**Persistência:**
- cadastro das bandejas
- grid, garra, referência, fiduciais

**Saída esperada:**
- bandejas configuradas para uso no ciclo automático

## Menu Calibrações

### CAL-MAP-01 — Calibração de Entrada

**Tela / Componente:** Menu Calibrações → `Calibração de Entrada...`  
**Evento:** clique e ações internas

**Controller provável:**
- controller de calibração de entrada

**Service / Manager provável:**
- manager/calibration service
- manager de posição

**Hardware / Visão:**
- câmera fiducial
- PLC controller

**Persistência:**
- referência de centro da bandeja

**Saída esperada:**
- centro da bandeja calibrado e salvo

---

### CAL-MAP-02 — Calibração de Offset da Garra

**Tela / Componente:** Menu Calibrações → `Calibrar Offset Garra...`  
**Evento:** clique e capturas

**Controller provável:**
- controller de offset da garra

**Service / Manager provável:**
- calibration service
- manager geométrico/offset

**Hardware / Visão:**
- câmera fiducial
- PLC controller

**Persistência:**
- ΔX, ΔY, ΔZ da garra

**Saída esperada:**
- offset salvo para uso em correção de posicionamento

---

### CAL-MAP-03 — Calibração CNC

**Tela / Componente:** Menu Calibrações → `Calibrar CNC...`  
**Evento:** clique / edição / aplicar

**Controller provável:**
- controller de calibração CNC

**Service / Manager provável:**
- calibration/settings service

**Hardware:**
- opcionalmente PLC/controller

**Persistência:**
- configuração de steps/mm

**Saída esperada:**
- conversão pulsos ↔ mm ajustada

---

### CAL-MAP-04 — Calibração de Foco

**Tela / Componente:** Menu Calibrações → `Calibrar Foco...`  
**Evento:** clique e ações internas

**Controller provável:**
- controller de calibração de foco

**Service / Manager provável:**
- calibration service
- camera manager

**Hardware / Visão:**
- câmeras
- PLC controller para pontos/movimento

**Persistência:**
- calibração de foco global ou local

**Saída esperada:**
- parâmetros de foco persistidos

---

### CAL-MAP-05 — Calibração FOV

**Tela / Componente:** Menu Calibrações → `Calibrar FOV...`  
**Evento:** clique / edição / salvar

**Controller provável:**
- controller de FOV

**Service / Manager provável:**
- calibration service

**Persistência:**
- modelo de campo de visão

**Saída esperada:**
- relação Z ↔ largura/altura visível registrada

---

### CAL-MAP-06 — Pontos Fiduciais

**Tela / Componente:** Menu Calibrações → `Pontos Fiduciais...`  
**Evento:** clique e ações internas

**Controller provável:**
- controller de fiduciais

**Service / Manager provável:**
- fiducial manager/service
- calibration service

**Hardware / Visão:**
- câmera
- PLC controller

**Persistência:**
- templates/imagens/posições/tolerância

**Saída esperada:**
- fiduciais configurados e disponíveis para alinhamento

---

### CAL-MAP-07 — Velocidades JOG

**Tela / Componente:** Menu Calibrações → `Velocidades JOG...`  
**Evento:** leitura/escrita

**Controller provável:**
- controller de velocidade/configuração

**Service / Manager provável:**
- PLC controller/driver
- settings manager

**Hardware:**
- CLP

**Persistência:**
- parâmetros de velocidade no CLP e possivelmente no software

**Saída esperada:**
- velocidades de JOG atualizadas
