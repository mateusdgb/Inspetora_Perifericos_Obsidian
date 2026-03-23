# Lógica do CLP

## Funções principais do CLP

O CLP é responsável por controlar:

- motores dos eixos
- sensores
- garra
- segurança da máquina

---

## Funções principais

### Homing

Executar referenciamento dos eixos X, Y e Z.

---

### Controle de Movimento

Permitir movimentação:

- manual
- automática

---

### Limites de Segurança

Garantir que os eixos não ultrapassem os limites permitidos.

---

### Controle da Garra

Executar comandos de:

- abrir garra
- fechar garra
- verificar captura da placa

---

### Comunicação com Interface Python

Receber comandos de:

- movimento
- início de ciclo
- parada

Enviar informações de:

- estado da máquina
- posição dos eixos
- alarmes

---

## Observações do Projeto Existente

O projeto já possui integração com CLP via Modbus TCP.

Arquivos principais:

- `hardware/plc_controller.py`
- `hardware/plc_driver.py`
- `hardware/simulation_plc_driver.py`

---

## Responsabilidades já observadas no software

O CLP e sua camada de controle já estão modelados para:

- movimentação manual dos eixos X, Y e Z
- leitura da posição atual
- homing
- execução de comandos de movimento
- parada de emergência
- operação em modo simulado

---

## Configurações observadas

No arquivo `core/settings.json` foram identificadas configurações para:

- limites de eixo
- posição home
- velocidades padrão
- índices/papéis de câmera
- posições de inspeção
- mapeamentos de I/O do PLC

---

## Limites e posições configuradas

Há parâmetros para:

- `axis_limits`
- `home_position`
- `inspection_positions`

Esses parâmetros devem ser ajustados à geometria real da Inspetora de Periféricos para evitar:

- colisão com vidro lateral
- colisão com câmeras
- deslocamentos fora da área útil

---

## Necessidades de adaptação identificadas

- revisar os limites reais dos 3 eixos
- validar homing real da máquina
- integrar automação da garra ao CLP
- revisar posições automáticas de inspeção e descarte
- incorporar restrições adicionais de segurança no eixo Z

---

## Documentos Relacionados

- [[fluxograma_segurança|Fluxograma de Segurança]]
- [[lista_sensores|Lista de Sensores]]
- [[lista_atuadores|Lista de Atuadores]]
- [[lacunas_para_adaptacao_inspetora|Lacunas para Adaptação]]