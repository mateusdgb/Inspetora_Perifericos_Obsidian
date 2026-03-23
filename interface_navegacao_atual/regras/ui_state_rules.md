# Regras de Estado da Interface

## Objetivo

Este documento descreve as regras de habilitação, desabilitação, visibilidade e uso dos componentes da interface da Inspetora de Periféricos.

Ele serve para:

- documentar o comportamento esperado da UI
- orientar refatoração futura da interface
- apoiar a definição de estados da aplicação
- alimentar LLM para geração de código com regras de habilitação corretas

---

## Estrutura de Regra

Cada regra deve informar:

- **Tela**
- **Componente**
- **Estado da UI**
- **Pré-condições**
- **Quando habilita**
- **Quando desabilita**
- **Ação ao interagir**
- **Observações**

---

## Estados globais relevantes

Os seguintes estados globais influenciam o comportamento da interface:

- aplicação iniciada
- programa não carregado
- programa carregado
- programa em edição
- câmera conectada
- câmera desconectada
- CLP conectado
- CLP desconectado
- modo simulação ativo
- modo real ativo
- ciclo em execução
- ciclo parado
- inspeção concluída
- alarme
- emergência

---

# Regras por Tela

## Tela Projeto

### Regra PROJ-STATE-01 — Botão Novo Programa

**Tela:** Projeto  
**Componente:** `Novo Programa`

**Estado da UI:** ação principal de criação

**Pré-condições:**
- aplicação ativa
- usuário com permissão adequada

**Quando habilita:**
- normalmente sempre disponível em modo de edição/configuração

**Quando desabilita:**
- durante operação crítica
- durante execução automática que bloqueie edição
- em estado de alarme grave, se a arquitetura decidir bloquear edição

**Ação ao interagir:**
- inicia fluxo de criação de programa

**Observações:**
- deve ser separado de estados operacionais de inspeção

---

### Regra PROJ-STATE-02 — Botão Carregar Programa

**Tela:** Projeto  
**Componente:** `Carregar Programa`

**Pré-condições:**
- existir ao menos um programa salvo

**Quando habilita:**
- com aplicação ativa
- fora de fluxo crítico de escrita/trava

**Quando desabilita:**
- quando não existem programas
- durante execução automática bloqueante
- quando houver edição não salva e a aplicação exigir confirmação

**Ação ao interagir:**
- abre seletor de programas

**Observações:**
- idealmente deve pedir confirmação se houver alterações pendentes

---

### Regra PROJ-STATE-03 — Botão Salvar Alterações

**Tela:** Projeto  
**Componente:** `Salvar Alterações`

**Pré-condições:**
- existir programa atual
- haver alterações pendentes ou contexto válido para persistência

**Quando habilita:**
- após criação/carregamento de programa
- após captura de imagem
- após mudança de região da placa
- após inclusão/edição/remoção de ROI
- após mudança em parâmetros da inspeção

**Quando desabilita:**
- quando não existe programa ativo
- quando não há alterações pendentes
- durante salvamento em andamento

**Ação ao interagir:**
- persiste alterações do programa atual

**Observações:**
- a UI futura pode indicar `dirty state` do programa

---

### Regra PROJ-STATE-04 — Abas de câmera da Tela Projeto

**Tela:** Projeto  
**Componente:** `Câmera 1`, `Câmera 2`, `Câmera 3`

**Pré-condições:**
- contexto do programa disponível

**Quando habilita:**
- após criação/carregamento de programa
- quando a arquitetura permitir edição por câmera

**Quando desabilita:**
- quando não existe programa ativo
- quando a câmera correspondente não faz parte do contexto carregado
- durante fluxo que exija confirmação antes da troca

**Ação ao interagir:**
- troca o contexto ativo da câmera

**Observações:**
- a troca deve preservar ou salvar contexto da câmera anterior

---

### Regra PROJ-STATE-05 — Subaba Imagem

**Tela:** Projeto  
**Componente:** `Imagem`

**Quando habilita:**
- normalmente sempre, após existir contexto mínimo da tela

**Quando desabilita:**
- raramente
- apenas se a aplicação bloquear edição por modo/estado

**Ação ao interagir:**
- mostra contexto de captura/edição visual da imagem

---

### Regra PROJ-STATE-06 — Subaba Inspeção

**Tela:** Projeto  
**Componente:** `Inspeção`

**Pré-condições:**
- programa ativo
- câmera selecionada

**Quando habilita:**
- após criação/carregamento do programa
- idealmente após existir imagem/captura válida da câmera

**Quando desabilita:**
- quando não existe programa ativo
- quando a câmera atual não tem contexto suficiente
- durante bloqueios de edição

**Ação ao interagir:**
- abre painel de configuração dos parâmetros de inspeção da câmera/itens

**Observações:**
- no estado atual, a subaba exibe parâmetros como threshold, % mínimo e similaridade

---

### Regra PROJ-STATE-07 — Botão Capturar Imagem

**Tela:** Projeto  
**Componente:** `Capturar Imagem`

**Pré-condições:**
- programa ativo
- câmera ativa disponível
- hardware ou simulação funcionando

**Quando habilita:**
- após existir contexto de programa
- com câmera disponível

**Quando desabilita:**
- sem programa
- sem câmera
- durante captura em andamento
- durante erro grave de comunicação com câmera

**Ação ao interagir:**
- captura imagem da câmera ativa

---

### Regra PROJ-STATE-08 — Botão Definir Região da Placa

**Tela:** Projeto  
**Componente:** `Definir Região da Placa`

**Pré-condições:**
- imagem capturada ou carregada
- programa ativo

**Quando habilita:**
- após haver imagem válida no painel

**Quando desabilita:**
- sem imagem
- durante modo de desenho de ROI já ativo
- durante salvamento/bloqueio de edição

**Ação ao interagir:**
- entra em modo de seleção da região da placa

---

### Regra PROJ-STATE-09 — Botão Desenhar ROI (+)

**Tela:** Projeto  
**Componente:** `Desenhar ROI (+)`

**Pré-condições:**
- imagem válida
- programa ativo
- idealmente região da placa já definida

**Quando habilita:**
- após captura de imagem
- após existência de contexto de inspeção mínimo

**Quando desabilita:**
- sem imagem
- sem programa
- durante outro modo de desenho
- quando a UI exigir primeiro a definição da região da placa

**Ação ao interagir:**
- entra em modo de anotação de ROI

---

### Regra PROJ-STATE-10 — Botão Concluir

**Tela:** Projeto  
**Componente:** `Concluir`

**Pré-condições:**
- programa ativo
- integridade mínima do programa atendida

**Quando habilita:**
- após criação/carregamento de programa
- idealmente após salvar ou quando houver dados mínimos válidos

**Quando desabilita:**
- programa inexistente
- programa incompleto
- salvamento em andamento

**Ação ao interagir:**
- finaliza edição do programa

---

### Regra PROJ-STATE-11 — Painel de movimentação manual

**Tela:** Projeto / Câmera Fiducial / Calibração  
**Componente:** controles X/Y/Z, STOP, Abrir, Fechar, Passo, Contínuo, Home

**Pré-condições:**
- CLP conectado ou simulação ativa
- eixos disponíveis
- estado seguro

**Quando habilita:**
- hardware pronto ou simulado
- sem alarme crítico

**Quando desabilita:**
- CLP desconectado, sem simulação
- emergência
- estado de bloqueio
- rotina automática exclusiva em andamento

**Ação ao interagir:**
- envia comando de movimentação ou controle da garra

**Observações:**
- regras de segurança e limites devem ser obrigatórias

---

## Tela Inspeção

### Regra INSP-STATE-01 — Botão Carregar

**Tela:** Inspeção  
**Componente:** `Carregar`

**Quando habilita:**
- quando houver programas/contextos disponíveis

**Quando desabilita:**
- durante operação que não permita troca de programa

---

### Regra INSP-STATE-02 — Botão Iniciar Ciclo

**Tela:** Inspeção  
**Componente:** `Iniciar Ciclo`

**Pré-condições:**
- programa carregado
- CLP pronto
- câmeras disponíveis
- sem alarme

**Quando habilita:**
- sistema pronto para execução

**Quando desabilita:**
- sem programa
- sem hardware
- durante ciclo em andamento
- em alarme/emergência

---

### Regra INSP-STATE-03 — Botão Parar

**Tela:** Inspeção  
**Componente:** `Parar`

**Quando habilita:**
- durante ciclo/execução interrompível

**Quando desabilita:**
- sistema ocioso
- nenhuma operação ativa

---

### Regra INSP-STATE-04 — Botão Inspecionar

**Tela:** Inspeção  
**Componente:** `Inspecionar`

**Pré-condições:**
- contexto carregado
- câmeras prontas
- dados mínimos disponíveis

**Quando habilita:**
- quando for possível rodar inspeção manual ou assistida

**Quando desabilita:**
- sem programa
- durante inspeção em andamento
- em falha crítica

---

### Regra INSP-STATE-05 — Botões Aprovar/Reprovar Peça

**Tela:** Inspeção  
**Componente:** `Aprovar Peça`, `Reprovar Peça`

**Pré-condições:**
- existir peça em contexto
- decisão manual permitida
- inspeção concluída ou estado compatível

**Quando habilita:**
- após inspeção/manual review
- quando a arquitetura permitir fechamento manual

**Quando desabilita:**
- antes de existir resultado/contexto
- após decisão já tomada
- durante ciclo sem revisão manual

---

## Tela Câmera Fiducial

### Regra FID-STATE-01 — Botão Ligar

**Tela:** Câmera Fiducial  
**Componente:** `Ligar`

**Quando habilita:**
- câmera ainda não conectada
- dispositivo disponível

**Quando desabilita:**
- câmera já ligada
- tentativa de conexão em andamento

---

### Regra FID-STATE-02 — Botões de posição

**Tela:** Câmera Fiducial  
**Componente:** `Adicionar posição atual`, `Inserir nova posição`, `Editar posição`, `Remover posição`

**Pré-condições:**
- contexto fiducial carregado ou em edição

**Quando habilita:**
- quando a tela estiver em modo de edição de programa fiducial

**Quando desabilita:**
- sem programa/contexto
- sem item selecionado no caso de editar/remover

---

### Regra FID-STATE-03 — Botões Salvar Programa / Carregar Programa / Executar

**Tela:** Câmera Fiducial  
**Componente:** `Salvar Programa`, `Carregar Programa`, `Executar`

**Quando habilita:**
- conforme existência de contexto e validade da sequência

**Quando desabilita:**
- sem programa
- sem posições suficientes
- hardware indisponível para execução

---

## Menu Configurações / CLP

### Regra CONF-STATE-01 — Conexão CLP

**Tela:** Diálogo Configuração CLP  
**Componente:** `Conectar`, `Testar Comunicação`

**Quando habilita:**
- parâmetros mínimos preenchidos

**Quando desabilita:**
- tentativa em andamento
- campos obrigatórios inválidos

---

---

## Menu Calibrações

### Regra CAL-STATE-01 — Itens do menu Calibrações

**Tela:** Menu Calibrações  
**Componente:** itens do menu

**Quando habilita:**
- aplicação ativa
- usuário com permissão de calibração/engenharia

**Quando desabilita:**
- ciclo automático crítico em execução, se a arquitetura bloquear calibração durante produção
- emergência
- modo operacional restrito

**Ação ao interagir:**
- abre a tela de calibração correspondente

---

## Calibração de Entrada

### Regra CAL-STATE-02 — Capturar Ponto 1

**Tela:** Calibração de Entrada  
**Componente:** `Capturar Ponto 1`

**Pré-condições:**
- tela aberta
- posição atual válida

**Quando habilita:**
- sempre que for possível ler coordenadas

**Quando desabilita:**
- hardware indisponível
- emergência

---

### Regra CAL-STATE-03 — Capturar Ponto 2

**Tela:** Calibração de Entrada  
**Componente:** `Capturar Ponto 2`

**Pré-condições:**
- idealmente Ponto 1 já capturado
- posição válida

**Quando habilita:**
- após Ponto 1 ou conforme a lógica atual da tela

**Quando desabilita:**
- sem contexto válido
- emergência

---

### Regra CAL-STATE-04 — Calcular e Salvar Centro da Bandeja

**Tela:** Calibração de Entrada  
**Componente:** `Calcular e Salvar`

**Pré-condições:**
- Ponto 1 e Ponto 2 capturados

**Quando habilita:**
- após os dois pontos existirem

**Quando desabilita:**
- qualquer ponto ausente
- salvamento em andamento

---

## Calibração de Offset da Garra

### Regra CAL-STATE-05 — Capturas da Garra/Câmera

**Tela:** Calibração Offset Garra  
**Componente:** capturas de referência

**Pré-condições:**
- câmera fiducial selecionada ou ativa
- posição atual válida

**Quando habilita:**
- com preview e hardware disponíveis

**Quando desabilita:**
- sem câmera
- sem posição
- emergência

---

### Regra CAL-STATE-06 — Salvar Offset

**Tela:** Calibração Offset Garra  
**Componente:** salvar/finalizar

**Pré-condições:**
- pontos mínimos capturados
- cálculo válido

**Quando habilita:**
- após completar as capturas necessárias

**Quando desabilita:**
- dados incompletos
- cálculo inconsistente

---

## Calibração CNC

### Regra CAL-STATE-07 — Aplicar ao Controlador

**Tela:** Calibração CNC  
**Componente:** `Aplicar ao Controlador`

**Pré-condições:**
- resultado de steps/mm válido

**Quando habilita:**
- após preenchimento correto dos campos

**Quando desabilita:**
- campos inválidos
- controlador indisponível

---

### Regra CAL-STATE-08 — Salvar e Fechar CNC

**Tela:** Calibração CNC  
**Componente:** `Salvar e Fechar`

**Quando habilita:**
- configuração válida

**Quando desabilita:**
- dados inválidos
- operação de gravação em andamento

---

## Calibração de Foco

### Regra CAL-STATE-09 — Live/Foto

**Tela:** Calibração de Foco  
**Componente:** botões de live/foto

**Quando habilita:**
- câmera disponível
- contexto de aba ativo

**Quando desabilita:**
- câmera indisponível
- captura em andamento, se houver trava

---

### Regra CAL-STATE-10 — Ajuste de Foco

**Tela:** Calibração de Foco  
**Componente:** slider de foco

**Quando habilita:**
- contexto de câmera carregado

**Quando desabilita:**
- sem câmera/contexto
- durante operação bloqueante

---

### Regra CAL-STATE-11 — Salvar Calibração de Foco

**Tela:** Calibração de Foco  
**Componente:** `Salvar Calibração`

**Pré-condições:**
- escopo selecionado
- parâmetros válidos

**Quando habilita:**
- após existir alteração relevante

**Quando desabilita:**
- sem mudanças
- sem escopo
- gravação em andamento

---

## Calibração FOV

### Regra CAL-STATE-12 — Salvar FOV

**Tela:** Calibração FOV  
**Componente:** `Salvar`

**Pré-condições:**
- campos Z, largura e altura preenchidos validamente

**Quando habilita:**
- após entrada válida dos parâmetros

**Quando desabilita:**
- dados inconsistentes
- gravação em andamento

---

## Pontos Fiduciais

### Regra CAL-STATE-13 — Capturar Fiducial

**Tela:** Pontos Fiduciais  
**Componente:** `Capturar`

**Pré-condições:**
- preview disponível
- posição válida
- câmera definida

**Quando habilita:**
- com contexto completo do fiducial

**Quando desabilita:**
- sem câmera
- sem preview
- emergência

---

### Regra CAL-STATE-14 — Ir Para Fiducial

**Tela:** Pontos Fiduciais  
**Componente:** `Ir Para`

**Pré-condições:**
- fiducial salvo

**Quando habilita:**
- após existir posição associada ao fiducial

**Quando desabilita:**
- sem posição salva
- hardware indisponível

---

### Regra CAL-STATE-15 — Salvar Fiduciais

**Tela:** Pontos Fiduciais  
**Componente:** `Salvar`

**Quando habilita:**
- após existir configuração mínima válida

**Quando desabilita:**
- sem fiduciais válidos
- salvamento em andamento

---

## Velocidades JOG

### Regra CAL-STATE-16 — Ler do CLP

**Tela:** Velocidades JOG  
**Componente:** `Ler do CLP`

**Quando habilita:**
- CLP acessível
- tela ativa

**Quando desabilita:**
- CLP indisponível
- leitura em andamento

---

### Regra CAL-STATE-17 — Escrever no CLP

**Tela:** Velocidades JOG  
**Componente:** `Escrever no CLP`

**Pré-condições:**
- valores válidos preenchidos

**Quando habilita:**
- CLP acessível
- configuração válida

**Quando desabilita:**
- CLP offline
- valores inválidos
- escrita em andamento

---

## Observações finais

As regras acima devem ser refinadas futuramente com base em:

- análise do código atual
- testes reais da interface
- comportamento observado durante navegação completa
- decisões de arquitetura da futura reimplementação