# Modelo de Eventos da Interface

## Objetivo

Descrever os eventos principais da interface da Inspetora de Periféricos, relacionando interações do usuário com:

- comportamento esperado da UI
- ações do sistema
- regras de negócio
- persistência
- integrações com hardware, visão computacional e CLP

Este documento serve como base para:

- entendimento da interface atual
- reorganização da arquitetura futura
- alimentação de LLM para geração de código

Fonte de verdade externa do estado atual:

- [[estado_atual_codigo]]

---

## Estrutura de descrição de evento

Cada evento da interface deve ser entendido pelos seguintes campos:

- **Tela**
- **Componente**
- **Evento**
- **Ação do Usuário**
- **Pré-condições**
- **Ação Esperada do Sistema**
- **Camadas Envolvidas**
- **Saída na Interface**
- **Persistência**
- **Erros Possíveis**
- **Pontos em Aberto**

---

## Índice de Eventos

### Tela Projeto

- [[#Evento PROJ-01 — Novo Programa]]
- [[#Evento PROJ-02 — Carregar Programa]]
- [[#Evento PROJ-03 — Salvar Alterações]]
- [[#Evento PROJ-04 — Selecionar câmera do Projeto]]
- [[#Evento PROJ-05 — Capturar Imagem]]
- [[#Evento PROJ-06 — Definir Região da Placa]]
- [[#Evento PROJ-07 — Desenhar ROI]]
- [[#Evento PROJ-08 — Concluir Programa]]
- [[#Evento PROJ-09 — Movimentação manual na tela Projeto]]
- [[#Evento PROJ-10 — Ir para Home]]

### Tela Inspeção

- [[#Evento INSP-01 — Selecionar câmera de preview]]
- [[#Evento INSP-02 — Carregar programa ou contexto de inspeção]]
- [[#Evento INSP-03 — Iniciar Ciclo]]
- [[#Evento INSP-04 — Parar Ciclo]]
- [[#Evento INSP-05 — Inspecionar]]
- [[#Evento INSP-06 — Navegar pelas falhas]]
- [[#Evento INSP-07 — Aprovar Peça]]
- [[#Evento INSP-08 — Reprovar Peça]]
- [[# Evento INSP-09 — Programação Rápida]]
- [[# Evento INSP-10 — Definir Janela Azul]]
- [[# Evento INSP-11 — Adicionar Inspeção]]
- [[# Evento INSP-12 — Aplicar Configuração de Inspeção]]
- [[# Evento INSP-13 — Aplicar Similaridade]]

### Tela Câmera Fiducial

- [[#Evento FID-01 — Ligar câmera fiducial]]
- [[#Evento FID-02 — Movimentação manual na fiducial]]
- [[#Evento FID-03 — Adicionar posição atual]]
- [[#Evento FID-04 — Inserir nova posição]]
- [[#Evento FID-05 — Editar posição]]
- [[#Evento FID-06 — Remover posição]]
- [[#Evento FID-07 — Salvar programa fiducial]]
- [[#Evento FID-08 — Carregar programa fiducial]]
- [[#Evento FID-09 — Executar programa fiducial]]
  
### Menu Configurações / Diálogos

- [[#Evento CONF-01 — Alterar tema]]
- [[#Evento CONF-02 — Abrir configuração de simulação]]
- [[#Evento CONF-03 — Salvar configuração de simulação]]
- [[#Evento CONF-04 — Abrir configuração de câmeras]]
- [[#Evento CONF-05 — Selecionar câmera física]]
- [[#Evento CONF-06 — Iniciar ou parar preview de câmera]]
- [[#Evento CONF-07 — Definir papel lógico da câmera]]
- [[#Evento CONF-08 — Ajustar parâmetros de imagem]]
- [[#Evento CONF-09 — Aplicar ou salvar configuração de câmera]]
- [[#Evento CONF-10 — Abrir configuração CLP]]
- [[#Evento CONF-11 — Testar comunicação CLP]]
- [[#Evento CONF-12 — Conectar ou desconectar CLP]]
- [[#Evento CONF-13 — Exportar log CLP]]
- [[#Evento CONF-14 — Abrir cadastro de bandejas]]
- [[#Evento CONF-15 — Criar, duplicar ou excluir bandeja]]
- [[#Evento CONF-16 — Editar detalhes da bandeja]]
- [[#Evento CONF-17 — Ensinar posição da bandeja]]
- [[#Evento CONF-18 — Configurar fiduciais da bandeja]]
- [[#Evento CONF-19 — Salvar bandeja]]
- [[#Evento CONF-20 — Testar posições ou preview da bandeja]]

### Menu Calibrações / Diálogos

- [[#Evento CAL-01 — Abrir calibração de entrada]]
- [[#Evento CAL-02 — Capturar ponto da calibração de entrada]]
- [[#Evento CAL-03 — Calcular e salvar centro da bandeja]]
- [[#Evento CAL-04 — Abrir calibração de offset da garra]]
- [[#Evento CAL-05 — Capturar pontos do offset da garra]]
- [[#Evento CAL-06 — Calcular e salvar offset]]
- [[#Evento CAL-07 — Abrir calibração CNC]]
- [[#Evento CAL-08 — Alterar parâmetros CNC]]
- [[#Evento CAL-09 — Aplicar ou salvar calibração CNC]]
- [[#Evento CAL-10 — Abrir calibração de foco]]
- [[#Evento CAL-11 — Selecionar câmera na calibração de foco]]
- [[#Evento CAL-12 — Ativar live ou foto na calibração de foco]]
- [[#Evento CAL-13 — Ajustar foco]]
- [[#Evento CAL-14 — Ir para Ponto A ou B]]
- [[#Evento CAL-15 — Salvar calibração de foco]]
- [[#Evento CAL-16 — Abrir calibração FOV]]
- [[#|Evento CAL-17 — Editar parâmetros de FOV]]
- [[#Evento CAL-18 — Salvar calibração FOV]]
- [[#Evento CAL-19 — Abrir configuração de pontos fiduciais]]
- [[#Evento CAL-20 — Capturar fiducial]]
- [[#Evento CAL-21 — Ir para fiducial]]
- [[#Evento CAL-22 — Salvar fiduciais]]
- [[#Evento CAL-23 — Abrir velocidades JOG]]
- [[#Evento CAL-24 — Ler velocidades do CLP]]
- [[#Evento CAL-25 — Escrever velocidades no CLP]]

### Menu Calibrações / Diálogos

- [[#evento-cal-01--abrir-calibracao-de-entrada]]
- [[#evento-cal-02--capturar-ponto-da-calibracao-de-entrada]]
- [[#evento-cal-03--calcular-e-salvar-centro-da-bandeja]]
- [[#evento-cal-04--abrir-calibracao-de-offset-da-garra]]
- [[#evento-cal-05--capturar-pontos-do-offset-da-garra]]
- [[#evento-cal-06--calcular-e-salvar-offset]]
- [[#evento-cal-07--abrir-calibracao-cnc]]
- [[#evento-cal-08--alterar-parametros-cnc]]
- [[#evento-cal-09--aplicar-ou-salvar-calibracao-cnc]]
- [[#evento-cal-10--abrir-calibracao-de-foco]]
- [[#evento-cal-11--selecionar-camera-na-calibracao-de-foco]]
- [[#evento-cal-12--ativar-live-ou-foto-na-calibracao-de-foco]]
- [[#evento-cal-13--ajustar-foco]]
- [[#evento-cal-14--ir-para-ponto-a-ou-b]]
- [[#evento-cal-15--salvar-calibracao-de-foco]]
- [[#evento-cal-16--abrir-calibracao-fov]]
- [[#evento-cal-17--editar-parametros-de-fov]]
- [[#evento-cal-18--salvar-calibracao-fov]]
- [[#evento-cal-19--abrir-configuracao-de-pontos-fiduciais]]
- [[#evento-cal-20--capturar-fiducial]]
- [[#evento-cal-21--ir-para-fiducial]]
- [[#evento-cal-22--salvar-fiduciais]]
- [[#evento-cal-23--abrir-velocidades-jog]]
- [[#evento-cal-24--ler-velocidades-do-clp]]
- [[#evento-cal-25--escrever-velocidades-no-clp]]
---

## Tela Projeto

### Evento PROJ-01 — Novo Programa

**Tela:** Projeto  
**Componente:** Botão `Novo Programa`  
**Evento:** clique

**Ação do Usuário:**  
Usuário solicita a criação de um novo programa de inspeção.

**Pré-condições:**
- aplicação em estado operacional
- usuário com permissão compatível
- nenhuma operação crítica em andamento

**Ação Esperada do Sistema:**
1. abrir fluxo de criação de programa
2. solicitar nome do programa
3. validar se o nome já existe
4. criar estrutura inicial do programa
5. preparar a tela para edição

**Camadas Envolvidas:**
- UI da tela Projeto
- controller de projeto
- manager/service de programas
- persistência em diretórios/JSON/imagens

**Saída na Interface:**
- programa atual passa a existir no contexto
- nome do programa pode ser exibido
- ações de captura/edição ficam habilitadas

**Persistência:**
- criação de estrutura inicial do programa

**Erros Possíveis:**
- nome duplicado
- falha ao criar diretório/arquivo
- nome inválido

**Pontos em Aberto:**
- formato exato do diálogo de criação
- campos obrigatórios além do nome

**Documento Relacionado:**  
[[acao_novo_programa|Ação Novo Programa]]

---

### Evento PROJ-02 — Carregar Programa

**Tela:** Projeto  
**Componente:** Botão `Carregar Programa`  
**Evento:** clique

**Ação do Usuário:**  
Usuário deseja abrir um programa já existente.

**Pré-condições:**
- existência de programas salvos
- sistema em estado seguro para troca de contexto

**Ação Esperada do Sistema:**
1. abrir seletor/lista de programas
2. carregar metadados do programa
3. restaurar câmera atual, imagens, ROIs e posições relacionadas
4. refletir o estado carregado na interface

**Camadas Envolvidas:**
- UI da tela Projeto
- controller de projeto
- program manager
- persistência

**Saída na Interface:**
- programa carregado visualmente
- imagem/ROIs/posições restauradas

**Persistência:**
- leitura de dados previamente salvos

**Erros Possíveis:**
- programa corrompido
- programa incompleto
- arquivos ausentes

**Pontos em Aberto:**
- se carrega o pacote completo ou apenas contexto parcial da câmera ativa

---

### Evento PROJ-03 — Salvar Alterações

**Tela:** Projeto  
**Componente:** Botão `Salvar Alterações`  
**Evento:** clique

**Ação do Usuário:**  
Usuário deseja persistir as mudanças realizadas no programa atual.

**Pré-condições:**
- existir programa carregado ou criado
- haver dados válidos para persistência

**Ação Esperada do Sistema:**
1. validar o estado atual do programa
2. salvar imagens, regiões, ROIs, posições e metadados
3. atualizar marcadores internos de estado salvo

**Camadas Envolvidas:**
- UI
- controller de projeto
- managers de imagem/projeto/inspeção
- persistência

**Saída na Interface:**
- feedback de sucesso ou erro
- possível remoção do estado “alterações pendentes”

**Persistência:**
- escrita em estrutura de projeto

**Erros Possíveis:**
- falha de disco
- inconsistência de ROI
- programa sem nome/contexto

**Pontos em Aberto:**
- diferença exata entre “Salvar Alterações” e “Concluir”

---

### Evento PROJ-04 — Selecionar câmera do Projeto

**Tela:** Projeto  
**Componente:** Abas `Câmera 1`, `Câmera 2`, `Câmera 3`  
**Evento:** clique

**Ação do Usuário:**  
Usuário alterna o contexto de edição entre as câmeras de inspeção.

**Pré-condições:**
- existir tela carregada
- câmera mapeada no sistema

**Ação Esperada do Sistema:**
1. trocar o contexto ativo da câmera
2. atualizar a área de imagem
3. carregar ROIs/placa/posições relacionados à câmera selecionada
4. atualizar ferramentas disponíveis

**Camadas Envolvidas:**
- UI
- controller de projeto
- project/program manager

**Saída na Interface:**
- aba ativa destacada
- imagem e dados da câmera correspondente exibidos

**Persistência:**
- normalmente leitura de dados
- possivelmente gravação de contexto atual antes da troca

**Erros Possíveis:**
- câmera sem dados
- falha ao restaurar contexto da câmera

**Pontos em Aberto:**
- detalhes de persistência do contexto antes da troca de aba

**Observação confirmada:**
- `Câmera 1` = `top`
- `Câmera 2` = `bottom`
- `Câmera 3` = `side`

---

### Evento PROJ-05 — Capturar Imagem

**Tela:** Projeto  
**Componente:** Botão `Capturar Imagem`  
**Evento:** clique

**Ação do Usuário:**  
Usuário solicita captura da imagem da câmera selecionada.

**Pré-condições:**
- câmera ativa disponível
- programa aberto
- posição física adequada

**Ação Esperada do Sistema:**
1. capturar frame da câmera ativa
2. exibir a imagem no painel
3. associar a captura ao programa e à câmera
4. liberar etapas posteriores de definição de placa e ROI

**Camadas Envolvidas:**
- UI
- controller de runtime/projeto
- camera manager
- persistência de imagem

**Saída na Interface:**
- imagem exibida
- botões dependentes podem ser habilitados

**Persistência:**
- imagem pode ser salva imediatamente ou mantida em buffer até salvar alterações

**Erros Possíveis:**
- câmera desconectada
- frame inválido
- falha de gravação

**Pontos em Aberto:**
- captura síncrona ou assíncrona
- se substitui imagem anterior ou cria versão nova

---

### Evento PROJ-06 — Definir Região da Placa

**Tela:** Projeto  
**Componente:** Botão `Definir Região da Placa`  
**Evento:** clique

**Ação do Usuário:**  
Usuário entra no modo de marcação da região da placa.

**Pré-condições:**
- imagem já capturada
- programa ativo

**Ação Esperada do Sistema:**
1. entrar no modo de seleção da área da placa
2. permitir marcação visual
3. registrar as coordenadas da região
4. associar a região ao contexto câmera/programa

**Camadas Envolvidas:**
- UI gráfica de anotação
- controller de região
- persistência de metadados do projeto

**Saída na Interface:**
- região destacada visualmente
- contexto pronto para ROIs internas

**Persistência:**
- metadados de bounding box/região

**Erros Possíveis:**
- seleção inválida
- ausência de imagem

**Pontos em Aberto:**
- se a região pode ser editada depois
- se existe apenas uma região por câmera

---

### Evento PROJ-07 — Desenhar ROI

**Tela:** Projeto  
**Componente:** Botão `Desenhar ROI (+)`  
**Evento:** clique

**Ação do Usuário:**  
Usuário solicita criação de uma nova ROI de inspeção.

**Pré-condições:**
- imagem existente
- programa ativo
- idealmente região da placa já definida

**Ação Esperada do Sistema:**
1. entrar em modo de anotação de ROI
2. permitir desenhar área
3. solicitar ou associar nome/tipo do item
4. salvar ROI no programa da câmera atual

**Camadas Envolvidas:**
- UI gráfica
- controller de regiões/componentes
- persistência do projeto

**Saída na Interface:**
- ROI visível sobre a imagem
- lista de itens do programa enriquecida

**Persistência:**
- gravação de ROI e metadados

**Erros Possíveis:**
- ROI fora da área válida
- sobreposição inválida
- ausência de contexto ativo

**Pontos em Aberto:**
- metadados obrigatórios de cada ROI
- tipo de componente associado

---

### Evento PROJ-08 — Concluir Programa

**Tela:** Projeto  
**Componente:** Botão `Concluir`  
**Evento:** clique

**Ação do Usuário:**  
Usuário finaliza a edição do programa atual.

**Pré-condições:**
- programa em edição
- dados mínimos obrigatórios presentes

**Ação Esperada do Sistema:**
1. validar integridade mínima do programa
2. salvar estado final
3. encerrar modo de edição
4. disponibilizar o programa para uso em inspeção

**Camadas Envolvidas:**
- UI
- controller de projeto
- program manager
- persistência

**Saída na Interface:**
- feedback de conclusão
- possível mudança de tela/estado

**Persistência:**
- persistência final do programa

**Erros Possíveis:**
- programa incompleto
- falha ao salvar

**Pontos em Aberto:**
- critérios mínimos para conclusão

---

### Evento PROJ-09 — Movimentação manual na tela Projeto

**Tela:** Projeto  
**Componente:** Painel de movimentação  
**Evento:** clique em direção / stop / abrir / fechar / modo passo/contínuo

**Ação do Usuário:**  
Usuário movimenta a máquina ou aciona a garra durante a preparação do programa.

**Pré-condições:**
- CLP conectado ou modo simulação ativo
- eixos habilitados
- sistema sem alarme crítico

**Ação Esperada do Sistema:**
1. converter interação da UI em comando de movimento
2. enviar comando ao controlador de hardware
3. atualizar posições X, Y, Z
4. respeitar limites e regiões seguras

**Camadas Envolvidas:**
- UI
- controller de hardware/movimento
- PLC controller/driver
- safety validator

**Saída na Interface:**
- indicadores de eixo atualizados
- feedback de movimento

**Persistência:**
- normalmente não
- eventualmente pode registrar posição usada em lista de captura

**Erros Possíveis:**
- CLP offline
- limite excedido
- colisão prevista
- eixo não referenciado

**Pontos em Aberto:**
- comportamento exato de contínuo versus passo
- semântica dos botões Abrir/Fechar em cada tela

---

### Evento PROJ-10 — Ir para Home

**Tela:** Projeto  
**Componente:** Botão `Ir para Zero (Home)`  
**Evento:** clique

**Ação do Usuário:**  
Usuário solicita retorno ao zero/home.

**Pré-condições:**
- hardware conectado ou simulado
- eixo referenciável
- sistema em condição segura

**Ação Esperada do Sistema:**
1. iniciar rotina de retorno/home
2. atualizar posições durante o processo
3. encerrar em posição home válida

**Camadas Envolvidas:**
- UI
- controller de movimento
- PLC controller/driver
- lógica de homing

**Saída na Interface:**
- eixos atualizados
- status de operação atualizado

**Persistência:**
- normalmente não

**Erros Possíveis:**
- falha de homing
- sensor inconsistente
- intertravamento de segurança

**Pontos em Aberto:**
- se o botão executa homing completo ou apenas goto home lógico

---

## Tela Inspeção

### Evento INSP-01 — Selecionar câmera de preview

**Tela:** Inspeção  
**Componente:** Abas `TOP`, `BOTTOM`, `SIDE`  
**Evento:** clique

**Ação do Usuário:**  
Usuário alterna a câmera de visualização no preview de inspeção.

**Pré-condições:**
- tela de inspeção ativa
- câmera configurada no sistema

**Ação Esperada do Sistema:**
1. mudar a aba ativa
2. atualizar preview
3. atualizar serial/status da câmera
4. manter restante do contexto da inspeção

**Camadas Envolvidas:**
- UI
- controller de inspeção/runtime
- camera manager

**Saída na Interface:**
- preview da câmera escolhida

**Persistência:**
- não obrigatória

**Erros Possíveis:**
- câmera indisponível
- preview indisponível

---

### Evento INSP-02 — Carregar programa ou contexto de inspeção

**Tela:** Inspeção  
**Componente:** Botão `Carregar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário deseja carregar o programa ou contexto necessário para inspecionar.

**Pré-condições:**
- existência de programa válido

**Ação Esperada do Sistema:**
1. abrir seleção de programa/contexto
2. carregar dados da inspeção
3. atualizar nome do programa e estado
4. habilitar operações posteriores

**Camadas Envolvidas:**
- UI
- inspection controller/service
- program manager

**Saída na Interface:**
- nome do programa exibido
- status da inspeção atualizado

**Persistência:**
- leitura do programa

**Erros Possíveis:**
- programa ausente
- inconsistência de dados

**Pontos em Aberto:**
- se carrega apenas programa ou também ordem/serial/lote

---

### Evento INSP-03 — Iniciar Ciclo

**Tela:** Inspeção  
**Componente:** Botão `Iniciar Ciclo`  
**Evento:** clique

**Ação do Usuário:**  
Usuário inicia o fluxo automatizado/operacional da inspeção.

**Pré-condições:**
- programa carregado
- câmeras disponíveis
- CLP pronto
- sistema fora de alarme

**Ação Esperada do Sistema:**
1. validar pré-condições
2. iniciar máquina de estados do ciclo
3. atualizar status atual
4. iniciar ou preparar deslocamentos/capturas

**Camadas Envolvidas:**
- UI
- machine cycle controller
- inspection runtime controller
- hardware orchestration
- inspection service

**Saída na Interface:**
- estado muda de idle para execução
- progresso começa a refletir o ciclo

**Persistência:**
- possível início de rastreabilidade/ciclo

**Erros Possíveis:**
- programa não carregado
- CLP desconectado
- câmera indisponível
- pré-condição não atendida

**Pontos em Aberto:**
- diferença operacional exata entre Iniciar Ciclo e Inspecionar

---

### Evento INSP-04 — Parar Ciclo

**Tela:** Inspeção  
**Componente:** Botão `Parar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário interrompe o fluxo em execução.

**Pré-condições:**
- ciclo em andamento ou estado interrompível

**Ação Esperada do Sistema:**
1. solicitar parada segura
2. atualizar estado
3. preservar informações relevantes do ciclo

**Camadas Envolvidas:**
- UI
- machine cycle controller
- hardware control

**Saída na Interface:**
- estado de pausa/parada
- botões reavaliados

**Persistência:**
- possível registro de ciclo interrompido

**Erros Possíveis:**
- parada em estado inconsistente

---

### Evento INSP-05 — Inspecionar

**Tela:** Inspeção  
**Componente:** Botão `Inspecionar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário solicita a execução da rotina de inspeção.

**Pré-condições:**
- programa carregado
- imagens ou hardware em condição válida
- sistema apto para inspecionar

**Ação Esperada do Sistema:**
1. capturar ou recuperar imagens necessárias
2. executar comparação/inspeção
3. gerar lista de falhas
4. atualizar resultado preliminar

**Camadas Envolvidas:**
- UI
- inspection runtime controller
- inspection service
- comparador/peripheral comparator
- câmeras

**Saída na Interface:**
- falhas exibidas
- contadores atualizados
- decisão preliminar disponível

**Persistência:**
- possível rastreabilidade da execução

**Erros Possíveis:**
- falha de captura
- falha de comparação
- programa incompleto

**Pontos em Aberto:**
- se esta ação é manual e separada do ciclo automático

---

### Evento INSP-06 — Navegar pelas falhas

**Tela:** Inspeção  
**Componente:** Botões `Anterior` e `Próximo`  
**Evento:** clique

**Ação do Usuário:**  
Usuário navega entre falhas detectadas.

**Pré-condições:**
- existir lista de falhas

**Ação Esperada do Sistema:**
1. alterar índice da falha corrente
2. atualizar imagem/recorte visualizado
3. atualizar câmera, posição e descrição do erro

**Camadas Envolvidas:**
- UI
- controller de inspeção
- dados temporários do resultado

**Saída na Interface:**
- falha atual alterada na visualização

**Persistência:**
- geralmente não

**Erros Possíveis:**
- lista vazia
- índice inválido

---

### Evento INSP-07 — Aprovar Peça

**Tela:** Inspeção  
**Componente:** Botão `Aprovar Peça`  
**Evento:** clique

**Ação do Usuário:**  
Usuário confirma aprovação da peça.

**Pré-condições:**
- peça em contexto
- decisão manual permitida
- estado válido para fechamento

**Ação Esperada do Sistema:**
1. registrar aprovação
2. atualizar contadores
3. persistir resultado
4. seguir fluxo de descarte OK ou fechamento da peça

**Camadas Envolvidas:**
- UI
- controller de inspeção/ciclo
- persistência/rastreabilidade

**Saída na Interface:**
- total/OK/NOK atualizados
- contexto pronto para próxima peça

**Persistência:**
- registro de rastreabilidade e decisão

**Erros Possíveis:**
- peça sem contexto
- estado inválido

---

### Evento INSP-08 — Reprovar Peça

**Tela:** Inspeção  
**Componente:** Botão `Reprovar Peça`  
**Evento:** clique

**Ação do Usuário:**  
Usuário confirma reprovação da peça.

**Pré-condições:**
- peça em contexto
- estado válido para decisão final

**Ação Esperada do Sistema:**
1. registrar reprovação
2. atualizar contadores
3. persistir falhas e decisão
4. seguir fluxo de descarte NG ou fechamento da peça

**Camadas Envolvidas:**
- UI
- controller de inspeção/ciclo
- rastreabilidade/persistência

**Saída na Interface:**
- total/OK/NOK atualizados
- falhas preservadas no histórico

**Persistência:**
- registro de reprovação e falhas

**Erros Possíveis:**
- ausência de peça/contexto
- estado inválido

---
### Evento INSP-09 — Programação Rápida

**Tela:** Projeto  
**Componente:** Botão `Programação Rápida` na subaba `Inspeção`  
**Evento:** clique

**Ação do Usuário:**  
Usuário deseja configurar inspeções de forma mais rápida ou assistida.

**Pré-condições:**
- programa ativo
- câmera/contexto ativo

**Ação Esperada do Sistema:**
1. abrir fluxo simplificado ou preset de inspeção
2. preencher parâmetros automaticamente ou semi-automaticamente
3. permitir revisão posterior

**Camadas Envolvidas:**
- UI
- controller de configuração de inspeção
- inspection manager/service

**Saída na Interface:**
- parâmetros preenchidos ou inspeção criada

**Persistência:**
- em memória e/ou após aplicar/salvar

**Erros Possíveis:**
- falta de contexto válido

**Pontos em Aberto:**
- comportamento exato ainda não confirmado

---

### Evento INSP-10 — Definir Janela Azul

**Tela:** Projeto  
**Componente:** Botão `Definir Janela Azul`  
**Evento:** clique

**Ação do Usuário:**  
Usuário define uma janela especial de inspeção.

**Pré-condições:**
- imagem/contexto ativo

**Ação Esperada do Sistema:**
1. entrar em modo de seleção da janela
2. registrar coordenadas da janela azul
3. associar ao item/regra atual

**Camadas Envolvidas:**
- UI gráfica
- controller de inspeção/região
- persistência do programa

**Saída na Interface:**
- janela visualmente marcada
- contexto atualizado

**Persistência:**
- metadados da janela

**Erros Possíveis:**
- ausência de imagem
- seleção inválida

**Pontos em Aberto:**
- finalidade exata da janela azul

---

### Evento INSP-11 — Adicionar Inspeção

**Tela:** Projeto  
**Componente:** Botão `Adicionar Inspeção`  
**Evento:** clique

**Ação do Usuário:**  
Usuário cria uma nova configuração de inspeção.

**Pré-condições:**
- programa ativo
- câmera ativa
- idealmente imagem/contexto selecionado

**Ação Esperada do Sistema:**
1. criar nova entrada/regra de inspeção
2. preparar campos para parametrização
3. associar ao contexto atual

**Camadas Envolvidas:**
- UI
- inspection controller
- inspection manager/service

**Saída na Interface:**
- nova inspeção disponível para edição

**Persistência:**
- após aplicar/salvar

**Erros Possíveis:**
- contexto incompleto

---

### Evento INSP-12 — Aplicar Configuração de Inspeção

**Tela:** Projeto  
**Componente:** Botão `Aplicar Config`  
**Evento:** clique

**Ação do Usuário:**  
Usuário aplica os parâmetros configurados para a inspeção atual.

**Pré-condições:**
- existir inspeção ou contexto selecionado
- campos válidos

**Ação Esperada do Sistema:**
1. validar threshold, polaridade, % mínimo e demais parâmetros
2. aplicar ao item/regra atual
3. atualizar estado interno do programa

**Camadas Envolvidas:**
- UI
- inspection controller
- inspection manager/service
- persistência em memória

**Saída na Interface:**
- configuração aplicada com feedback visual

**Persistência:**
- definitiva ao salvar alterações do programa

**Erros Possíveis:**
- valor inválido
- contexto inexistente

---

### Evento INSP-13 — Aplicar Similaridade

**Tela:** Projeto  
**Componente:** Botão `Aplicar Similaridade`  
**Evento:** clique

**Ação do Usuário:**  
Usuário aplica o critério de similaridade configurado.

**Pré-condições:**
- contexto válido
- campo Similaridade preenchido

**Ação Esperada do Sistema:**
1. validar valor de similaridade
2. associar o valor à regra atual
3. atualizar o contexto de inspeção

**Camadas Envolvidas:**
- UI
- inspection controller/service
- comparador de periféricos

**Saída na Interface:**
- valor ativo no contexto

**Persistência:**
- definitiva ao salvar o programa

**Erros Possíveis:**
- valor fora do intervalo esperado
## Tela Câmera Fiducial

### Evento FID-01 — Ligar câmera fiducial

**Tela:** Câmera Fiducial  
**Componente:** Botão `Ligar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário tenta conectar/ativar a câmera fiducial.

**Pré-condições:**
- dispositivo disponível
- configuração correta da câmera

**Ação Esperada do Sistema:**
1. tentar abrir conexão com a câmera
2. atualizar status textual/visual
3. exibir preview se houver sucesso

**Camadas Envolvidas:**
- UI
- camera manager
- controller da fiducial

**Saída na Interface:**
- status muda de desconectada para conectada
- preview ativo

**Persistência:**
- normalmente não

**Erros Possíveis:**
- câmera ausente
- índice incorreto
- falha de driver

---

### Evento FID-02 — Movimentação manual na fiducial

**Tela:** Câmera Fiducial  
**Componente:** Painel de movimentação  
**Evento:** clique em comandos de eixo e garra

**Ação do Usuário:**  
Usuário move a estrutura para alinhamento/setup da fiducial.

**Pré-condições:**
- CLP disponível ou modo simulado
- limites válidos

**Ação Esperada do Sistema:**
1. enviar comandos de movimento
2. atualizar posições X/Y/Z
3. respeitar limites e segurança

**Camadas Envolvidas:**
- UI
- controller de hardware
- PLC controller
- safety validator

**Saída na Interface:**
- posições atualizadas

**Persistência:**
- não obrigatória

**Erros Possíveis:**
- CLP desconectado
- limite excedido

---

### Evento FID-03 — Adicionar posição atual

**Tela:** Câmera Fiducial  
**Componente:** Botão `Adicionar posição atual`  
**Evento:** clique

**Ação do Usuário:**  
Usuário deseja registrar a posição atual como ponto do programa fiducial.

**Pré-condições:**
- leitura válida de posição
- programa/contexto fiducial ativo

**Ação Esperada do Sistema:**
1. capturar coordenadas atuais
2. adicionar item na lista de posições
3. permitir salvar posteriormente

**Camadas Envolvidas:**
- UI
- controller de posições
- persistência de programa fiducial

**Saída na Interface:**
- nova posição visível na lista

**Persistência:**
- imediata ou em memória até salvar

**Erros Possíveis:**
- posição indisponível
- programa inexistente

---

### Evento FID-04 — Inserir nova posição

**Tela:** Câmera Fiducial  
**Componente:** Botão `Inserir nova posição`  
**Evento:** clique

**Ação do Usuário:**  
Usuário quer criar manualmente uma posição.

**Pré-condições:**
- contexto de edição ativo

**Ação Esperada do Sistema:**
1. abrir formulário ou modo de entrada manual
2. validar coordenadas
3. adicionar posição ao programa

**Camadas Envolvidas:**
- UI
- controller de posições
- persistência

**Saída na Interface:**
- posição aparece na lista

**Persistência:**
- em memória e/ou ao salvar

**Erros Possíveis:**
- coordenadas inválidas

---

### Evento FID-05 — Editar posição

**Tela:** Câmera Fiducial  
**Componente:** Botão `Editar posição`  
**Evento:** clique

**Ação do Usuário:**  
Usuário altera posição existente.

**Pré-condições:**
- item selecionado na lista

**Ação Esperada do Sistema:**
1. abrir edição do item
2. validar alterações
3. atualizar lista e contexto

**Camadas Envolvidas:**
- UI
- controller de posições
- persistência

**Saída na Interface:**
- posição atualizada visualmente

**Persistência:**
- posterior ou imediata

**Erros Possíveis:**
- nenhum item selecionado

---

### Evento FID-06 — Remover posição

**Tela:** Câmera Fiducial  
**Componente:** Botão `Remover posição`  
**Evento:** clique

**Ação do Usuário:**  
Usuário exclui uma posição cadastrada.

**Pré-condições:**
- item selecionado

**Ação Esperada do Sistema:**
1. remover posição do contexto atual
2. atualizar lista
3. refletir a exclusão no programa salvo quando persistido

**Camadas Envolvidas:**
- UI
- controller de posições
- persistência

**Saída na Interface:**
- item desaparece da lista

**Persistência:**
- ao salvar ou imediatamente

**Erros Possíveis:**
- item inexistente

---

### Evento FID-07 — Salvar programa fiducial

**Tela:** Câmera Fiducial  
**Componente:** Botão `Salvar Programa`  
**Evento:** clique

**Ação do Usuário:**  
Usuário persiste o conjunto de posições/configurações da fiducial.

**Pré-condições:**
- contexto fiducial carregado
- dados válidos

**Ação Esperada do Sistema:**
1. validar programa fiducial
2. salvar posições
3. registrar configuração associada

**Camadas Envolvidas:**
- UI
- controller/program manager
- persistência

**Saída na Interface:**
- feedback de sucesso/erro

**Persistência:**
- escrita de programa da fiducial

**Erros Possíveis:**
- sem programa carregado
- dados inválidos

---

### Evento FID-08 — Carregar programa fiducial

**Tela:** Câmera Fiducial  
**Componente:** Botão `Carregar Programa`  
**Evento:** clique

**Ação do Usuário:**  
Usuário restaura um programa fiducial salvo.

**Pré-condições:**
- haver programas disponíveis

**Ação Esperada do Sistema:**
1. abrir seletor de programa
2. carregar posições
3. atualizar a lista visual
4. restaurar contexto de execução

**Camadas Envolvidas:**
- UI
- controller/program manager
- persistência

**Saída na Interface:**
- posições carregadas aparecem na tela

**Persistência:**
- leitura de programa

**Erros Possíveis:**
- programa ausente/corrompido

---

### Evento FID-09 — Executar programa fiducial

**Tela:** Câmera Fiducial  
**Componente:** Botão `Executar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário executa a sequência ligada às posições da fiducial.

**Pré-condições:**
- programa fiducial válido
- hardware conectado

**Ação Esperada do Sistema:**
1. validar sequência
2. executar deslocamentos
3. atualizar estado e posição
4. concluir ou reportar erro

**Camadas Envolvidas:**
- UI
- controller de execução
- PLC/hardware
- possivelmente câmera fiducial

**Saída na Interface:**
- feedback de execução
- atualização das coordenadas

**Persistência:**
- opcional: log/estado da execução

**Erros Possíveis:**
- sequência inválida
- falha de hardware

---

## Menu Configurações / Diálogos

### Evento CONF-01 — Alterar tema

**Tela:** Menu Configurações  
**Componente:** submenu `Tema`  
**Evento:** seleção de opção

**Ação do Usuário:**  
Usuário escolhe Auto, Claro ou Escuro.

**Pré-condições:**
- aplicação ativa

**Ação Esperada do Sistema:**
1. aplicar o tema visual
2. atualizar aparência da interface
3. persistir preferência, se aplicável

**Camadas Envolvidas:**
- UI
- settings/theme manager

**Saída na Interface:**
- mudança visual imediata ou ao reiniciar

---

### Evento CONF-02 — Abrir configuração de simulação

**Tela:** Menu Configurações  
**Componente:** item `Simulação`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a configuração de simulação.

**Ação Esperada do Sistema:**
1. abrir diálogo de simulação
2. carregar configuração atual

---

### Evento CONF-03 — Salvar configuração de simulação

**Tela:** Configuração de Simulação  
**Componente:** `Salvar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário persiste o modo simulado e suas opções.

**Pré-condições:**
- parâmetros válidos

**Ação Esperada do Sistema:**
1. salvar modo simulado
2. salvar multiplicador/opções
3. atualizar comportamento do sistema

**Camadas Envolvidas:**
- UI
- settings manager
- hardware orchestration

---

### Evento CONF-04 — Abrir configuração de câmeras

**Tela:** Menu Configurações  
**Componente:** `Configurar Câmeras...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a configuração de câmeras.

**Ação Esperada do Sistema:**
1. abrir a tela de câmeras
2. listar dispositivos disponíveis
3. restaurar configuração atual

---

### Evento CONF-05 — Selecionar câmera física

**Tela:** Configuração de Câmeras  
**Componente:** dropdown de câmera  
**Evento:** seleção

**Ação do Usuário:**  
Usuário escolhe um dispositivo físico.

**Ação Esperada do Sistema:**
1. atualizar o dispositivo ativo
2. preparar preview e ajustes

---

### Evento CONF-06 — Iniciar ou parar preview de câmera

**Tela:** Configuração de Câmeras  
**Componente:** `Iniciar` / `Parar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário inicia ou encerra o preview.

**Ação Esperada do Sistema:**
1. abrir/fechar stream
2. atualizar preview

**Camadas Envolvidas:**
- UI
- camera manager

---

### Evento CONF-07 — Definir papel lógico da câmera

**Tela:** Configuração de Câmeras  
**Componente:** radio buttons do papel da câmera  
**Evento:** seleção

**Ação do Usuário:**  
Usuário define a função lógica da câmera.

**Ação Esperada do Sistema:**
1. associar papel ao dispositivo
2. atualizar contexto interno

---

### Evento CONF-08 — Ajustar parâmetros de imagem

**Tela:** Configuração de Câmeras  
**Componente:** sliders de imagem  
**Evento:** ajuste

**Ação do Usuário:**  
Usuário altera foco, exposição, brilho, contraste, saturação ou balanço branco.

**Ação Esperada do Sistema:**
1. atualizar parâmetros temporários
2. refletir no preview
3. preparar para aplicar/salvar

---

### Evento CONF-09 — Aplicar ou salvar configuração de câmera

**Tela:** Configuração de Câmeras  
**Componente:** `Aplicar`, `Salvar e Fechar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário confirma a configuração de câmera.

**Ação Esperada do Sistema:**
1. validar ajustes
2. aplicar ao contexto atual
3. persistir ao salvar e fechar

---

### Evento CONF-10 — Abrir configuração CLP

**Tela:** Menu Configurações  
**Componente:** `Conexão CLP...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a tela de CLP.

**Ação Esperada do Sistema:**
1. abrir a tela
2. carregar parâmetros salvos

---

### Evento CONF-11 — Testar comunicação CLP

**Tela:** Configuração CLP  
**Componente:** `Testar Comunicação`  
**Evento:** clique

**Ação do Usuário:**  
Usuário testa a comunicação.

**Ação Esperada do Sistema:**
1. tentar comunicação
2. registrar no log
3. informar sucesso ou falha

---

### Evento CONF-12 — Conectar ou desconectar CLP

**Tela:** Configuração CLP  
**Componente:** `Conectar` / `Desconectar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário altera o estado da conexão.

**Ação Esperada do Sistema:**
1. abrir ou encerrar a conexão
2. atualizar status e log

---

### Evento CONF-13 — Exportar log CLP

**Tela:** Configuração CLP  
**Componente:** `Exportar Log`  
**Evento:** clique

**Ação do Usuário:**  
Usuário exporta o log.

**Ação Esperada do Sistema:**
1. gerar arquivo de log
2. permitir armazenamento externo

---

### Evento CONF-14 — Abrir cadastro de bandejas

**Tela:** Menu Configurações  
**Componente:** `Cadastro de Bandejas...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a gestão de bandejas.

**Ação Esperada do Sistema:**
1. abrir a tela
2. carregar lista de bandejas

---

### Evento CONF-15 — Criar, duplicar ou excluir bandeja

**Tela:** Cadastro de Bandejas  
**Componente:** `+ Nova`, `Duplicar`, `Excluir`  
**Evento:** clique

**Ação do Usuário:**  
Usuário gerencia instâncias de bandeja.

**Ação Esperada do Sistema:**
1. criar novo contexto
2. duplicar bandeja atual
3. excluir bandeja selecionada, se permitido

---

### Evento CONF-16 — Editar detalhes da bandeja

**Tela:** Cadastro de Bandejas  
**Componente:** campos de detalhes  
**Evento:** edição

**Ação do Usuário:**  
Usuário altera grid, garra, tipo, nome etc.

**Ação Esperada do Sistema:**
1. atualizar modelo interno da bandeja
2. recalcular totais, se necessário

---

### Evento CONF-17 — Ensinar posição da bandeja

**Tela:** Cadastro de Bandejas  
**Componente:** `Ensinar Posição`  
**Evento:** clique

**Ação do Usuário:**  
Usuário captura posição de referência.

**Ação Esperada do Sistema:**
1. ler posição X Y Z atual
2. preencher referência da bandeja

---

### Evento CONF-18 — Configurar fiduciais da bandeja

**Tela:** Cadastro de Bandejas  
**Componente:** `Configurar Fiduciais...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a configuração de fiduciais da bandeja.

**Ação Esperada do Sistema:**
1. abrir a tela de fiduciais
2. associar ao cadastro atual

---

### Evento CONF-19 — Salvar bandeja

**Tela:** Cadastro de Bandejas  
**Componente:** `Salvar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário persiste a bandeja.

**Ação Esperada do Sistema:**
1. validar os campos
2. salvar cadastro

---

### Evento CONF-20 — Testar posições ou preview da bandeja

**Tela:** Cadastro de Bandejas  
**Componente:** `Testar Posições`, `Preview`  
**Evento:** clique

**Ação do Usuário:**  
Usuário quer visualizar/testar a geometria da bandeja.

**Ação Esperada do Sistema:**
1. usar a configuração da bandeja
2. mostrar ou testar as posições previstas

## Menu Calibrações / Diálogos

### Evento CAL-01 — Abrir calibração de entrada

**Tela:** Menu Calibrações  
**Componente:** Item `Calibração de Entrada...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a ferramenta para calibrar o centro da bandeja de entrada.

**Pré-condições:**
- aplicação ativa
- permissões compatíveis
- módulo de calibração disponível

**Ação Esperada do Sistema:**
1. abrir a tela de calibração de entrada
2. inicializar preview da câmera fiducial, se aplicável
3. preparar contexto de captura de pontos

**Camadas Envolvidas:**
- UI
- controller de calibração
- camera manager
- controller de movimento

**Saída na Interface:**
- diálogo/tela de calibração exibido

**Persistência:**
- normalmente apenas leitura inicial

**Erros Possíveis:**
- câmera indisponível
- módulo de calibração não carregado

---

### Evento CAL-02 — Capturar ponto da calibração de entrada

**Tela:** Calibração de Entrada  
**Componente:** `Capturar Ponto 1` / `Capturar Ponto 2`  
**Evento:** clique

**Ação do Usuário:**  
Usuário posiciona a máquina e captura um ponto de referência.

**Pré-condições:**
- posição válida disponível
- hardware conectado ou simulado
- tela aberta

**Ação Esperada do Sistema:**
1. ler posição atual X Y Z
2. associar ao ponto selecionado
3. exibir coordenadas capturadas

**Camadas Envolvidas:**
- UI
- controller de calibração
- PLC controller
- manager de posição

**Saída na Interface:**
- ponto preenchido na área de captura

**Persistência:**
- temporária até salvar

**Erros Possíveis:**
- posição indisponível
- leitura inválida de eixo

---

### Evento CAL-03 — Calcular e salvar centro da bandeja

**Tela:** Calibração de Entrada  
**Componente:** Botão `Calcular e Salvar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário solicita o cálculo do centro da bandeja.

**Pré-condições:**
- Ponto 1 e Ponto 2 capturados

**Ação Esperada do Sistema:**
1. calcular o centro a partir dos pontos
2. exibir o resultado
3. persistir a calibração

**Camadas Envolvidas:**
- UI
- service/controller de calibração
- persistência de configuração

**Saída na Interface:**
- centro disponível/confirmado
- feedback de sucesso

**Persistência:**
- escrita da referência da bandeja

**Erros Possíveis:**
- pontos ausentes
- falha ao salvar

---

### Evento CAL-04 — Abrir calibração de offset da garra

**Tela:** Menu Calibrações  
**Componente:** Item `Calibrar Offset Garra...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a ferramenta para calibrar o offset entre a garra e a câmera fiducial.

**Pré-condições:**
- aplicação ativa

**Ação Esperada do Sistema:**
1. abrir a tela de offset
2. preparar preview e controles jog
3. carregar contexto atual de offset, se existir

**Camadas Envolvidas:**
- UI
- controller de calibração
- camera manager
- PLC controller

**Saída na Interface:**
- diálogo/tela de offset exibido

---

### Evento CAL-05 — Capturar pontos do offset da garra

**Tela:** Calibração de Offset da Garra  
**Componente:** capturas de `Garra Esquerda`, `Garra Direita`, `Centro Câmera`  
**Evento:** clique

**Ação do Usuário:**  
Usuário captura os três referenciais necessários para o cálculo.

**Pré-condições:**
- preview/câmera disponível
- posição atual válida

**Ação Esperada do Sistema:**
1. ler coordenadas X Y Z
2. armazenar no ponto selecionado
3. atualizar painel de cálculo

**Camadas Envolvidas:**
- UI
- controller de calibração
- PLC controller
- manager de posição

**Saída na Interface:**
- pontos preenchidos visualmente

**Persistência:**
- temporária até cálculo/salvamento

**Erros Possíveis:**
- leitura de posição inválida
- câmera não alinhada corretamente

---

### Evento CAL-06 — Calcular e salvar offset

**Tela:** Calibração de Offset da Garra  
**Componente:** botão de salvar/finalizar  
**Evento:** clique

**Ação do Usuário:**  
Usuário finaliza a calibração de offset.

**Pré-condições:**
- pontos necessários capturados

**Ação Esperada do Sistema:**
1. calcular centro da garra
2. calcular ΔX, ΔY, ΔZ
3. persistir offset

**Camadas Envolvidas:**
- UI
- service/controller de calibração
- persistência de parâmetros

**Saída na Interface:**
- valores de offset confirmados

**Persistência:**
- gravação do offset

**Erros Possíveis:**
- pontos incompletos
- falha de persistência

---

### Evento CAL-07 — Abrir calibração CNC

**Tela:** Menu Calibrações  
**Componente:** Item `Calibrar CNC...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a tela de steps/mm.

**Pré-condições:**
- aplicação ativa

**Ação Esperada do Sistema:**
1. abrir tela CNC
2. carregar parâmetros atuais, se houver

**Camadas Envolvidas:**
- UI
- settings/calibration controller

**Saída na Interface:**
- diálogo CNC exibido

---

### Evento CAL-08 — Alterar parâmetros CNC

**Tela:** Calibração CNC  
**Componente:** campos de passos, microsteps, relação, passo do fuso  
**Evento:** edição

**Ação do Usuário:**  
Usuário informa ou altera parâmetros mecânicos.

**Pré-condições:**
- tela aberta

**Ação Esperada do Sistema:**
1. recalcular steps/mm
2. atualizar campo de resultado

**Camadas Envolvidas:**
- UI
- lógica local de cálculo
- controller de calibração

**Saída na Interface:**
- resultado atualizado em tempo real

**Persistência:**
- ainda não, até aplicar/salvar

**Erros Possíveis:**
- valores inválidos
- divisão por zero

---

### Evento CAL-09 — Aplicar ou salvar calibração CNC

**Tela:** Calibração CNC  
**Componente:** `Aplicar ao Controlador`, `Salvar e Fechar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário deseja gravar a calibração CNC.

**Pré-condições:**
- resultado válido calculado

**Ação Esperada do Sistema:**
1. aplicar ao controlador e/ou salvar configuração
2. encerrar tela, se aplicável

**Camadas Envolvidas:**
- UI
- controller de calibração
- PLC/settings manager

**Saída na Interface:**
- confirmação de aplicação/salvamento

**Persistência:**
- gravação de steps/mm

**Erros Possíveis:**
- controlador indisponível
- falha ao salvar

---

### Evento CAL-10 — Abrir calibração de foco

**Tela:** Menu Calibrações  
**Componente:** Item `Calibrar Foco...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a tela unificada de foco.

**Pré-condições:**
- aplicação ativa

**Ação Esperada do Sistema:**
1. abrir tela de foco
2. carregar câmeras e parâmetros existentes

**Camadas Envolvidas:**
- UI
- calibration controller
- camera manager

**Saída na Interface:**
- diálogo de foco exibido

---

### Evento CAL-11 — Selecionar câmera na calibração de foco

**Tela:** Calibração de Foco  
**Componente:** abas de câmera  
**Evento:** clique

**Ação do Usuário:**  
Usuário muda o contexto da câmera.

**Pré-condições:**
- diálogo aberto

**Ação Esperada do Sistema:**
1. trocar câmera ativa
2. atualizar preview e controles

**Camadas Envolvidas:**
- UI
- calibration controller
- camera manager

**Saída na Interface:**
- preview atualizado

---

### Evento CAL-12 — Ativar live ou foto na calibração de foco

**Tela:** Calibração de Foco  
**Componente:** botões `Live` / `Foto`  
**Evento:** clique

**Ação do Usuário:**  
Usuário quer visualizar stream ao vivo ou capturar quadro.

**Pré-condições:**
- câmera disponível

**Ação Esperada do Sistema:**
1. iniciar stream ou capturar imagem
2. atualizar preview

**Camadas Envolvidas:**
- UI
- camera manager
- calibration controller

**Saída na Interface:**
- preview atualizado

**Erros Possíveis:**
- câmera indisponível

---

### Evento CAL-13 — Ajustar foco

**Tela:** Calibração de Foco  
**Componente:** slider/valor de foco  
**Evento:** arraste/edição

**Ação do Usuário:**  
Usuário ajusta o parâmetro de foco.

**Pré-condições:**
- contexto de câmera ativo

**Ação Esperada do Sistema:**
1. atualizar valor de foco
2. refletir no contexto da calibração
3. preparar para salvamento

**Camadas Envolvidas:**
- UI
- calibration service/controller

**Saída na Interface:**
- valor e estado visual atualizados

---

### Evento CAL-14 — Ir para Ponto A ou B

**Tela:** Calibração de Foco  
**Componente:** `Ir Ponto A` / `Ir Ponto B`  
**Evento:** clique

**Ação do Usuário:**  
Usuário manda a máquina ir para ponto salvo da calibração.

**Pré-condições:**
- ponto definido
- hardware disponível

**Ação Esperada do Sistema:**
1. carregar coordenadas do ponto
2. executar movimento
3. atualizar posição

**Camadas Envolvidas:**
- UI
- calibration controller
- PLC controller

**Saída na Interface:**
- posição atualizada

**Erros Possíveis:**
- ponto não definido
- falha de movimento

---

### Evento CAL-15 — Salvar calibração de foco

**Tela:** Calibração de Foco  
**Componente:** `Salvar Calibração`  
**Evento:** clique

**Ação do Usuário:**  
Usuário persiste a calibração.

**Pré-condições:**
- parâmetros válidos
- escopo selecionado

**Ação Esperada do Sistema:**
1. validar dados
2. persistir no escopo global ou local
3. informar sucesso

**Camadas Envolvidas:**
- UI
- calibration service
- persistência

**Saída na Interface:**
- feedback visual

**Persistência:**
- gravação da calibração

**Erros Possíveis:**
- dados inválidos
- falha de gravação

---

### Evento CAL-16 — Abrir calibração FOV

**Tela:** Menu Calibrações  
**Componente:** Item `Calibrar FOV...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a tela de campo de visão.

**Pré-condições:**
- aplicação ativa

**Ação Esperada do Sistema:**
1. abrir diálogo de FOV
2. carregar parâmetros existentes, se houver

**Camadas Envolvidas:**
- UI
- calibration controller

**Saída na Interface:**
- diálogo exibido

---

### Evento CAL-17 — Editar parâmetros de FOV

**Tela:** Calibração FOV  
**Componente:** campos Z, largura visível, altura visível  
**Evento:** edição

**Ação do Usuário:**  
Usuário informa dados físicos medidos.

**Pré-condições:**
- diálogo aberto

**Ação Esperada do Sistema:**
1. aceitar/validar os campos
2. preparar o modelo de FOV

**Camadas Envolvidas:**
- UI
- controller/service de calibração

**Saída na Interface:**
- campos atualizados

**Erros Possíveis:**
- valores inválidos

---

### Evento CAL-18 — Salvar calibração FOV

**Tela:** Calibração FOV  
**Componente:** `Salvar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário salva os parâmetros do campo de visão.

**Pré-condições:**
- dados válidos preenchidos

**Ação Esperada do Sistema:**
1. persistir dados do FOV
2. fechar ou confirmar a gravação

**Camadas Envolvidas:**
- UI
- calibration service
- persistência

**Saída na Interface:**
- confirmação de salvamento

---

### Evento CAL-19 — Abrir configuração de pontos fiduciais

**Tela:** Menu Calibrações  
**Componente:** Item `Pontos Fiduciais...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a configuração dos fiduciais.

**Pré-condições:**
- aplicação ativa

**Ação Esperada do Sistema:**
1. abrir tela de fiduciais
2. carregar parâmetros e capturas existentes

**Camadas Envolvidas:**
- UI
- controller de fiduciais
- camera manager

**Saída na Interface:**
- tela de fiduciais exibida

---

### Evento CAL-20 — Capturar fiducial

**Tela:** Pontos Fiduciais  
**Componente:** `Capturar` de um fiducial  
**Evento:** clique

**Ação do Usuário:**  
Usuário captura a referência visual e espacial do fiducial.

**Pré-condições:**
- preview disponível
- posição válida da máquina

**Ação Esperada do Sistema:**
1. capturar imagem/template
2. salvar posição X Y Z
3. associar câmera e tolerância

**Camadas Envolvidas:**
- UI
- controller de fiduciais
- camera manager
- PLC controller

**Saída na Interface:**
- miniatura e posição atualizadas

---

### Evento CAL-21 — Ir para fiducial

**Tela:** Pontos Fiduciais  
**Componente:** `Ir Para`  
**Evento:** clique

**Ação do Usuário:**  
Usuário manda a máquina voltar para o fiducial salvo.

**Pré-condições:**
- fiducial salvo

**Ação Esperada do Sistema:**
1. carregar posição do fiducial
2. executar movimento
3. atualizar coordenadas

**Camadas Envolvidas:**
- UI
- controller de fiduciais
- PLC controller

**Saída na Interface:**
- máquina reposicionada

---

### Evento CAL-22 — Salvar fiduciais

**Tela:** Pontos Fiduciais  
**Componente:** `Salvar`  
**Evento:** clique

**Ação do Usuário:**  
Usuário persiste a configuração de fiduciais.

**Pré-condições:**
- fiduciais definidos

**Ação Esperada do Sistema:**
1. salvar templates, posições e parâmetros
2. atualizar configuração da bandeja

**Camadas Envolvidas:**
- UI
- controller de fiduciais
- persistência

**Saída na Interface:**
- confirmação de sucesso

---

### Evento CAL-23 — Abrir velocidades JOG

**Tela:** Menu Calibrações  
**Componente:** Item `Velocidades JOG...`  
**Evento:** clique

**Ação do Usuário:**  
Usuário abre a tela de velocidades manuais.

**Pré-condições:**
- aplicação ativa

**Ação Esperada do Sistema:**
1. abrir tela de JOG
2. preparar leitura/escrita com CLP

**Camadas Envolvidas:**
- UI
- controller de configuração
- PLC controller

**Saída na Interface:**
- tela de velocidades exibida

---

### Evento CAL-24 — Ler velocidades do CLP

**Tela:** Velocidades JOG  
**Componente:** `Ler do CLP`  
**Evento:** clique

**Ação do Usuário:**  
Usuário solicita leitura das velocidades atuais.

**Pré-condições:**
- CLP acessível

**Ação Esperada do Sistema:**
1. consultar CLP
2. preencher campos da tela

**Camadas Envolvidas:**
- UI
- PLC controller/driver

**Saída na Interface:**
- campos atualizados

**Erros Possíveis:**
- CLP offline
- falha de leitura

---

### Evento CAL-25 — Escrever velocidades no CLP

**Tela:** Velocidades JOG  
**Componente:** `Escrever no CLP`  
**Evento:** clique

**Ação do Usuário:**  
Usuário grava novos valores de velocidade.

**Pré-condições:**
- valores válidos preenchidos
- CLP acessível

**Ação Esperada do Sistema:**
1. validar dados
2. escrever no CLP
3. confirmar operação

**Camadas Envolvidas:**
- UI
- PLC controller/driver
- validation layer

**Saída na Interface:**
- feedback de sucesso/erro
