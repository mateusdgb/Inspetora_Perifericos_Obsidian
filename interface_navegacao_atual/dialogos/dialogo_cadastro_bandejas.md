# Diálogo: Cadastro de Bandejas

## Objetivo

Cadastrar e configurar bandejas usadas pela Inspetora de Periféricos.

As bandejas representam regiões organizadas onde peças podem ser:
- recebidas
- aprovadas
- reprovadas
- manipuladas em modo genérico

---

## Tipos observados

- **Todas**
- **Entrada**
- **Saída OK**
- **Saída NG**
- **Universal**

Na lista da esquerda aparecem exemplos como:
- Bandeja_entrada
- Bandeja_NG
- Bandeja_saida
- BandejaUniversal

---

## Estrutura da tela

### Painel esquerdo
Lista de bandejas cadastradas.

Botões inferiores:
- `+ Nova`
- `Duplicar`
- `Excluir`

---

### Painel direito — Detalhes

Campos observados:

#### Identificação
- **Nome**
- **Tipo**

---

### Seção `Grid`
Campos:
- **Linhas**
- **Colunas**
- **Espaç X**
- **Espaç Y**
- **Total**

#### O que isso significa
A bandeja é modelada como uma grade de posições.

- **Linhas** = quantidade de linhas de posições
- **Colunas** = quantidade de colunas
- **Espaç X** = distância entre posições no eixo X
- **Espaç Y** = distância entre posições no eixo Y
- **Total** = total de posições disponíveis

---

### Seção `Garra`
Campos:
- **Abertura**
- **Fechamento**

Esses valores representam parâmetros da garra associados ao uso daquela bandeja.

Interpretação provável:
- abertura necessária para pegar/soltar peça naquela bandeja
- fechamento mínimo operacional para captura segura

---

### Seção `Posição Referência`
Campos:
- **X**
- **Y**
- **Z**
- botão `Ensinar Posição`

#### O que significa
A bandeja possui uma posição de referência no espaço da máquina.

Essa posição serve como origem/base para calcular todas as outras casas do grid.

---

### Seção `Fiduciais`
- checkbox `Validar posicionamento`
- botão `Configurar Fiduciais...`

#### O que significa
Permite ativar validação por fiduciais para aquela bandeja, tornando o posicionamento mais robusto.

---

### Botões finais
- `Salvar`
- `Testar Posições`
- `Preview`

---

## Fluxo esperado de uso

1. criar ou selecionar bandeja
2. preencher nome e tipo
3. definir grid
4. ajustar parâmetros da garra
5. ensinar posição de referência
6. opcionalmente configurar fiduciais
7. salvar
8. opcionalmente testar posições ou abrir preview

---

## Importância no sistema

Essa tela é central para o fluxo automático da máquina, pois modela:
- onde estão as placas
- como a garra deve atuar
- como o sistema interpreta as posições da bandeja

---

## Pontos em aberto

- o que exatamente faz `Preview`
- o que exatamente faz `Testar Posições`
- se o tipo Universal é fallback genérico
- se a bandeja pode herdar fiduciais de outra configuração

---

## Ações relacionadas

- [[acao_abrir_cadastro_bandejas|Abrir Cadastro de Bandejas]]
- [[acao_nova_bandeja|Criar Nova Bandeja]]
- [[acao_ensinar_posicao_bandeja|Ensinar Posição da Bandeja]]
- [[acao_configurar_fiduciais_bandeja|Configurar Fiduciais da Bandeja]]
- [[acao_salvar_bandeja|Salvar Bandeja]]

## Fluxo relacionado

- [[interface_navegacao/fluxos/fluxo_cadastro_bandejas|Fluxo Cadastro de Bandejas]]