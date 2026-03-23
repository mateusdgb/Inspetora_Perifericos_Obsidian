# Diagrama de Estados da Máquina

## Objetivo

Descrever os estados principais de operação da Inspetora de Periféricos, servindo como base para implementação da lógica de controle no CLP, da interface de operação em Python e da integração com visão computacional.

---

# Descrição dos Estados

<details>
<summary><strong>Inicializando</strong></summary>

Estado executado no momento em que a máquina é energizada e seus módulos começam a ser carregados.

Durante esse estado o sistema inicializa:

- CLP
- Interface Python
- Câmeras
- Sensores

Após a inicialização completa, o sistema transita para o estado de **Homing**.

</details>


<details>
<summary><strong>Homing</strong></summary>

Estado responsável pelo referenciamento dos eixos X, Y e Z.

Nesse processo a máquina movimenta os eixos até encontrar seus sensores de referência para estabelecer a posição zero do sistema.

Caso ocorra falha de referenciamento, o sistema entra em estado de **Alarme**.

</details>


<details>
<summary><strong>Pronta</strong></summary>

Estado de espera da máquina.

A máquina permanece aguardando:

- início de ciclo automático
- ativação de modo manual
- entrada em modo manutenção

</details>


<details>
<summary><strong>Movimentação Manual</strong></summary>

Permite ao operador mover manualmente os eixos:

- X
- Y
- Z

Esse modo é utilizado para:

- setup
- calibração
- manutenção
- testes

</details>


<details>
<summary><strong>Posicionando para Captura</strong></summary>

A máquina desloca os eixos até a posição da próxima placa na bandeja de entrada.

A posição da placa pode ser validada através da câmera de alinhamento (fiducial).

</details>


<details>
<summary><strong>Ajustando Garra</strong></summary>

A garra ajusta sua abertura de acordo com a dimensão da placa detectada.

Esse ajuste pode utilizar:

- parâmetros definidos
- informações obtidas pela câmera de alinhamento

</details>


<details>
<summary><strong>Capturando Placa</strong></summary>

A garra realiza a captura física da placa.

Após o fechamento da garra, sensores ou validações devem confirmar que a placa foi capturada corretamente.

Caso a captura falhe, o sistema pode entrar em **Alarme**.

</details>


<details>
<summary><strong>Transportando para Inspeção</strong></summary>

A placa capturada é transportada até a posição das câmeras de inspeção.

Esse movimento envolve deslocamentos controlados nos eixos:

- X
- Y
- Z

Os limites de segurança devem ser respeitados para evitar colisões.

</details>


<details>
<summary><strong>Inspecionando</strong></summary>

As câmeras capturam imagens da placa.

O sistema de visão computacional executa a análise dos periféricos para verificar:

- presença
- posicionamento
- possíveis falhas de montagem

</details>


<details>
<summary><strong>Classificando</strong></summary>

O resultado da inspeção é interpretado pelo sistema.

A placa é classificada como:

- **Aprovada**
- **Reprovada**

Essa decisão define o destino da placa.

</details>


<details>
<summary><strong>Depositando Aprovada</strong></summary>

A placa classificada como aprovada é transportada até a bandeja de saída destinada às placas aprovadas.

Após a deposição, a garra é liberada.

</details>


<details>
<summary><strong>Depositando Reprovada</strong></summary>

A placa classificada como reprovada é transportada até a bandeja de saída destinada às placas reprovadas.

Esse processo permite separar automaticamente peças com defeito.

</details>


<details>
<summary><strong>Retornando para Origem</strong></summary>

A garra retorna para uma posição segura ou para a posição inicial de captura.

Se ainda houver placas disponíveis, o ciclo de inspeção recomeça.

</details>


<details>
<summary><strong>Alarme</strong></summary>

Estado acionado quando ocorre uma falha operacional.

Exemplos:

- falha de sensor
- erro de captura
- falha de movimentação
- erro de visão computacional

A máquina permanece parada até intervenção do operador.

</details>


<details>
<summary><strong>Emergência</strong></summary>

Estado acionado quando ocorre uma condição crítica de segurança.

Exemplos:

- botão de emergência pressionado
- colisão detectada
- risco ao operador

Todos os movimentos devem ser imediatamente interrompidos.

</details>


<details>
<summary><strong>Manutenção</strong></summary>

Estado destinado a intervenções técnicas.

Permite:

- calibração
- testes
- ajustes mecânicos
- validação de sensores

</details>


---

## Diagrama Mermaid

```mermaid
stateDiagram-v2
    [*] --> Inicializando

    Inicializando --> Homing : sistema ligado
    Homing --> Pronta : homing concluído
    Homing --> Alarme : falha de referenciamento

    Pronta --> Movimentacao_Manual : modo manual selecionado
    Movimentacao_Manual --> Pronta : sair do modo manual

    Pronta --> Posicionando_para_Captura : ciclo iniciado

    Posicionando_para_Captura --> Ajustando_Garra : placa detectada e posição válida
    Posicionando_para_Captura --> Alarme : posição inválida ou sensor inconsistente

    Ajustando_Garra --> Capturando_Placa : garra ajustada
    Ajustando_Garra --> Alarme : falha no ajuste

    Capturando_Placa --> Transportando_para_Inspecao : placa capturada
    Capturando_Placa --> Alarme : falha de captura

    Transportando_para_Inspecao --> Inspecionando : posição de inspeção atingida
    Transportando_para_Inspecao --> Alarme : falha de deslocamento ou risco de colisão

    Inspecionando --> Classificando : inspeção concluída
    Inspecionando --> Alarme : falha de câmera ou processamento

    Classificando --> Depositando_Aprovada : resultado aprovado
    Classificando --> Depositando_Reprovada : resultado reprovado

    Depositando_Aprovada --> Retornando_para_Origem : placa depositada
    Depositando_Reprovada --> Retornando_para_Origem : placa depositada

    Retornando_para_Origem --> Pronta : sem novas placas
    Retornando_para_Origem --> Posicionando_para_Captura : existe próxima placa

    Pronta --> Manutencao : modo manutenção selecionado
    Manutencao --> Pronta : manutenção encerrada

    Inicializando --> Emergencia : emergência acionada
    Homing --> Emergencia : emergência acionada
    Pronta --> Emergencia : emergência acionada
    Movimentacao_Manual --> Emergencia : emergência acionada
    Posicionando_para_Captura --> Emergencia : emergência acionada
    Ajustando_Garra --> Emergencia : emergência acionada
    Capturando_Placa --> Emergencia : emergência acionada
    Transportando_para_Inspecao --> Emergencia : emergência acionada
    Inspecionando --> Emergencia : emergência acionada
    Classificando --> Emergencia : emergência acionada
    Depositando_Aprovada --> Emergencia : emergência acionada
    Depositando_Reprovada --> Emergencia : emergência acionada
    Retornando_para_Origem --> Emergencia : emergência acionada
    Manutencao --> Emergencia : emergência acionada

    Emergencia --> Pronta : reset e condição segura restabelecida
    Alarme --> Pronta : falha reconhecida e reset realizado
```

---  

## Relação com os Estados Existentes no Código

O projeto modelo já possui enumeração central de estados em:

- `enums/cycle_state.py`

Os estados existentes no código incluem tanto estados de alto nível quanto estados operacionais, como:

- `IDLE`
- `VERIFICAR_PRE_CONDICOES`
- `VALIDAR_BANDEJA`
- `PICKUP_ENTRADA`
- `CAPTURA`
- `INSPECIONAR`
- `DECIDIR`
- `PLACE_OK`
- `PLACE_NG`
- `REGISTRAR`
- `LOADING`
- `POSITIONING`
- `FOCUSING`
- `CAPTURING`
- `INSPECTING`
- `DECIDING`
- `DEPOSITING_OK`
- `DEPOSITING_REJECT`
- `COMPLETE`
- `PAUSED`
- `ERROR`

Assim, temos aqui a representação de uma visão conceitual da máquina, enquanto o enum do projeto representa a visão operacional já implementada no software.
# Documentos Relacionados  
  
- [[visão_geral|Visão Geral]]  
- [[arquitetura_sistema|Arquitetura do Sistema]]  
- [[fluxograma_operacao|Fluxograma de Operação]]  
- [[fluxograma_segurança|Fluxograma de Segurança]]  
- [[lógica_clp|Lógica do CLP]]  
- [[lista_sensores|Lista de Sensores]]  
- [[lista_atuadores|Lista de Atuadores]]  
- [[visão_computacional|Visão Computacional]]