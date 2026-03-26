# Tela: Projeto

## Objetivo

Permitir criar, carregar, editar e manter programas de inspeção.

## Elementos observados

### Navegação da tela

- Aba principal: **Projeto**
- Abas de câmera do fluxo principal:
  - `Câmera 1` = alias de `top`
  - `Câmera 2` = alias de `bottom`
  - `Câmera 3` = alias de `side`
- A câmera `fiducial` não cria aba dentro da tela Projeto
- Subabas internas:
  - [[subaba_imagem|Subaba Imagem]]
  - [[subaba_inspecao|Subaba Inspeção]]

### Botões principais

- [[acao_novo_programa|Novo Programa]]
- [[acao_carregar_programa|Carregar Programa]]
- [[acao_salvar_alteracoes|Salvar Alterações]]

## Estado atual confirmado

- a tela Projeto cria contexto por câmera de inspeção, não por fiducial
- cada aba interna possui `Imagem` e `Inspeção`
- a configuração física das câmeras vem de `SettingsManager.camera_indices`
- a persistência do programa continua centralizada em `ProgramManager`

## Pontos ainda em aberto

- diferença exata do botão **Usar Esta**, se ainda estiver exposto no fluxo ativo
- detalhes finos de persistência das posições de captura por câmera

## Fluxos relacionados

- [[../../estado_atual_codigo|Estado Atual do Código]]
- [[fluxo_criar_programa|Fluxo Criar Programa]]
- [[acao_novo_programa|Ação Novo Programa]]
- [[acao_capturar_imagem|Ação Capturar Imagem]]
