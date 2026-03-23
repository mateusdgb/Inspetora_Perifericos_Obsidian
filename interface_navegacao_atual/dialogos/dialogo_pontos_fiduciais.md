# Diálogo: Pontos Fiduciais

## Objetivo

Cadastrar, capturar, testar e salvar os **fiduciais da bandeja**.

Fiducial é um ponto conhecido de referência visual e/ou geométrica.  
  
Na prática, ele serve para:  
- alinhar a bandeja  
- corrigir pequenas diferenças de posição  
- validar se a peça ou bandeja está onde deveria  
- criar base para ajuste fino por visão

---

## Conceito de Fiducial

Um **fiducial** é uma referência visual conhecida usada para:

- localização
- alinhamento
- correção geométrica
- validação de posição

Na prática, ele ajuda a máquina a saber onde está a bandeja ou a região de interesse no espaço físico.

---

## Estrutura da tela

### Painel de controles de movimentação

Permite movimentar a máquina até os pontos desejados.

### Preview da câmera (LIVE)

Mostra a imagem ao vivo usada para capturar os fiduciais.

### Configurações do algoritmo

Campos observados:

- **Threshold**
- **Área Busca**
- **Método**

### Painéis laterais de fiduciais

Pelo menos dois blocos foram observados:

- **Fiducial 1**
- **Fiducial 2**

Cada um possui:

- preview/local de captura
- posição X/Y/Z
- seleção de câmera
- tolerância
- botão **Ir Para**
- botão **Capturar**

### Ações finais

- botão de teste/detecção
- **Salvar**
- **Cancelar**

---

## Significado dos parâmetros

### Threshold
Limiar usado pelo algoritmo de detecção.

Ajuda a separar visualmente o fiducial do restante da imagem.

### Área Busca
Tamanho ou região de busca do algoritmo.

Quanto maior a área, maior a região onde o sistema procurará o fiducial.

### Método
Algoritmo usado para detectar a referência.

Exemplo observado:
- **Template Matching**

---

## Significado dos campos por fiducial

### Posição X/Y/Z
Coordenadas associadas ao fiducial.

### Câmera
Indica qual câmera será usada para esse fiducial.

### Tolerância
Margem aceitável para considerar o fiducial corretamente localizado.

### Ir Para
Leva a máquina à posição associada ao fiducial.

### Capturar
Registra ou atualiza a referência visual do fiducial.

---

## Interpretação funcional

A tela permite ensinar ao sistema onde estão fiduciais relevantes da bandeja e como detectá-los.

Isso pode ser usado para:

- alinhamento inicial da bandeja
- compensação de pequenas variações
- validação de posicionamento

---

## Fluxo de uso esperado

1. mover a máquina até o fiducial desejado
2. ajustar preview e parâmetros
3. clicar em **Capturar**
4. repetir para outros fiduciais
5. testar detecção
6. salvar configuração

---

## Pontos em aberto

- quantos fiduciais o sistema suporta
- se cada fiducial pertence à bandeja, ao projeto ou à máquina
- como o teste de detecção se integra com o fluxo automático
  
---  
  
## Ações relacionadas  
  
- [[acao_abrir_pontos_fiduciais|Abrir Configuração de Pontos Fiduciais]]  
- [[interface_navegacao/acoes/acao_capturar_fiducial|Capturar Fiducial]]  
- [[interface_navegacao/acoes/acao_ir_para_fiducial|Ir para Fiducial]]  
- [[interface_navegacao/acoes/acao_salvar_fiduciais|Salvar Fiduciais]]  
  
## Fluxo relacionado  
  
- [[interface_navegacao/fluxos/fluxo_pontos_fiduciais|Fluxo Pontos Fiduciais]]