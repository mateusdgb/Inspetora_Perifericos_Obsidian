# Bandejas e Regiões de Segurança

## Objetivo

Registrar a base já existente no software para modelar bandejas e zonas de segurança.

---

## Bandejas

O projeto já possui um serviço específico para bandejas:

- `services/tray_manager.py`

E um cadastro persistido em:

- `cadastros/bandejas.json`

---

## Tipos de bandeja já observados

O `TrayManager` já prevê:

- `entrada`
- `saida_ok`
- `saida_ng`
- `universal`

Esse modelo combina bem com a lógica da Inspetora de Periféricos, que deve possuir pelo menos:

- bandeja de entrada
- bandeja de saída para aprovadas
- bandeja de saída para reprovadas

---

## Regiões de segurança

O projeto já possui serviço específico para segurança espacial:

- `services/safety_validator.py`

Cadastro persistido em:

- `cadastros/regioes_seguranca.json`

---

## Tipos de região já previstos

O validador suporta:

- `cilindro`
- `caixa`

Essas regiões podem ser usadas para modelar áreas proibidas da máquina, como:

- vidro lateral
- zona ocupada pelas câmeras
- zona das bandejas
- limites do cabeçote e da garra

---

## Importância para a máquina real

As falhas observadas em teste mostram que essa parte é crítica, especialmente para evitar:

- batida no vidro lateral
- colisão com câmera
- deslocamento perigoso no eixo Z

---

## Recomendações

- mapear fisicamente as zonas proibidas reais
- converter essas zonas para o cadastro do sistema
- validar todas as rotas automáticas contra essas regiões
- usar o validador tanto em movimento manual assistido quanto em movimentos automáticos

---

## Documentos Relacionados

- [[fluxograma_segurança|Fluxograma de Segurança]]
- [[lógica_clp|Lógica do CLP]]
- [[lista_sensores|Lista de Sensores]]
- [[lista_atuadores|Lista de Atuadores]]