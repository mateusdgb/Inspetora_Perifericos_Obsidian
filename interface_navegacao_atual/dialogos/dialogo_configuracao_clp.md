# Diálogo: Configuração de Conexão CLP

## Objetivo

Permitir configurar e testar a comunicação com o PLC.

## Campos observados

- Status
- botão Conectar
- botão Testar Comunicação
- Endereço IP
- Porta Modbus
- Timeout
- checkbox Conectar automaticamente ao iniciar
- Log de Comunicação
- botão Limpar Log
- botão Exportar Log
- botão Fechar

## Fluxo funcional esperado

1. usuário informa IP, porta e timeout
2. usuário pode testar a comunicação
3. usuário pode conectar
4. sistema atualiza status
5. logs são exibidos no painel
6. configuração pode ser persistida

## Pontos a confirmar depois

- diferença exata entre Testar Comunicação e Conectar
- onde a configuração é salva
- formato do log exportado
- se o status é atualizado em tempo real

## Fluxo relacionado

- [[fluxo_configuracao_clp|Fluxo Configuração CLP]]