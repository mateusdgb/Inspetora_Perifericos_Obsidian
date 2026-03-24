# Diálogo: Configurações de Simulação

## Objetivo

Configurar o funcionamento do sistema em **modo de simulação**.

O modo de simulação permite usar a aplicação sem depender do hardware físico real.

---

## Para que serve o modo simulação

Serve para:
- desenvolvimento
- testes de navegação
- testes de lógica
- validação inicial de interface
- demonstração sem máquina real

---

## Elementos observados

### Seção `Modo de Simulação`
- checkbox `Ativar Modo de Simulação`
- campo `Multiplicador de Velocidade`

### Seção `Opções de Simulação`
- `Simular Posições XYZ`
- `Simular Capturas de Câmera`
- `Log de Simulação`

### Botões
- `Cancelar`
- `Salvar`

---

## Significado dos campos

### Ativar Modo de Simulação
Ativa o comportamento simulado do sistema.

Quando ativo, o sistema passa a responder como se o hardware estivesse presente.

### Multiplicador de Velocidade
Fator que altera a velocidade da simulação.

Exemplo:
- 1.00x = velocidade normal simulada
- valores maiores = simulação mais rápida
- valores menores = simulação mais lenta

### Simular Posições XYZ
Permite que o sistema gere posições simuladas dos eixos.

### Simular Capturas de Câmera
Permite que o sistema simule imagens/capturas mesmo sem câmera real.

### Log de Simulação
Ativa registro dos eventos simulados para depuração e análise.

---

## Aviso observado

A tela informa que o modo simulação **não substitui testes com hardware real**.

Isso é importante para evitar falsa sensação de validação completa.

---

## Fluxo esperado de uso

1. abrir a tela
2. ativar ou desativar simulação
3. configurar multiplicador de velocidade
4. escolher quais recursos simular
5. salvar

---

## Importância no sistema

Essa configuração afeta:
- drivers usados
- respostas de movimento
- captura de câmeras
- comportamento de testes

---

## Pontos em aberto

- se a simulação vale para a aplicação inteira ou apenas para alguns módulos
- se o estado é persistido globalmente
- se o log de simulação fica em arquivo

---

## Ações relacionadas

- [[acao_abrir_configuracao_simulacao|Abrir Configuração de Simulação]]
- [[acao_salvar_configuracao_simulacao|Salvar Configuração de Simulação]]
