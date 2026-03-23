# Diálogo: Velocidades JOG

## Objetivo

Configurar as velocidades de movimentação manual da máquina.

Essas velocidades influenciam a operação de JOG dos eixos e da garra.

---

## Conceito de JOG

**JOG** é a movimentação manual, normalmente usada para:

- setup  
- calibração  
- manutenção  
- ajustes finos  
  
Pode ocorrer em:  
- movimentos positivos  
- movimentos negativos  
- abertura e fechamento da garra

---

## Estrutura da tela

### Painel Eixos XYZ

Para cada eixo:

- Y
- X
- Z

existem campos para:

- **Positivo (+)**
- **Negativo (-)**

### Painel Garra (G)

Campos observados:

- **Abrir (G+)**
- **Fechar (G-)**

### Botões

- **Ler do CLP**
- **Escrever no CLP**
- **Fechar**

---

## Significado dos campos

### Positivo (+)
Velocidade usada ao movimentar o eixo no sentido positivo.

### Negativo (-)
Velocidade usada ao movimentar o eixo no sentido negativo.

### Abrir (G+)  
Velocidade de abertura da garra.  
  
### Fechar (G-)  
Velocidade de fechamento da garra.  
  
### p/s  
Pulsos por segundo.  
É a unidade de velocidade usada pelo controle.

---

## Interpretação funcional

Essa tela permite ajustar a agressividade ou suavidade do movimento manual.

Isso é muito importante porque velocidades inadequadas podem causar:

- risco mecânico
- perda de precisão
- desconforto de operação
- impacto em calibração

---

## Fluxo de uso esperado

1. clicar em **Ler do CLP**
2. verificar os valores atuais
3. editar os campos desejados
4. clicar em **Escrever no CLP**
5. fechar o diálogo


---

## Pontos em aberto

- unidade real dos valores exibidos
- se os valores também ficam salvos em arquivo local
- se há limites máximos/mínimos validados pela UI

---
## Ações relacionadas  
  
- [[acao_abrir_velocidades_jog|Abrir Velocidades JOG]]  
- [[interface_navegacao/acoes/acao_ler_velocidades_clp|Ler Velocidades do CLP]]  
- [[interface_navegacao/acoes/acao_escrever_velocidades_clp|Escrever Velocidades no CLP]]  
  
## Fluxo relacionado  
  
- [[interface_navegacao/fluxos/fluxo_velocidades_jog|Fluxo Velocidades JOG]]