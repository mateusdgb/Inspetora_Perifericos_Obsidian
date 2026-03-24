# Diálogo: Configuração de Câmeras

## Objetivo

Esta tela configura os dispositivos de câmera usados pelo sistema e define o papel lógico de cada um.

Ela também permite ajustar parâmetros básicos de imagem.

---

## Conceito importante: câmera física x papel lógico

Uma câmera física é o dispositivo real conectado ao computador.

Um papel lógico é a função daquela câmera no sistema.

Exemplos de papel lógico observados:
- **Top (Superior)**
- **Bottom (Inferior)**
- **Side (Lateral)**
- **Fiducial**
- **Desabilitar**

Isso significa que o sistema pode associar uma câmera física a uma função específica dentro da inspeção.

---

## Elementos observados

### Seleção de câmera
Campo dropdown com lista de dispositivos detectados.

### Navegação
- `Anterior`
- `Próxima`

Sugere configuração sequencial de múltiplas câmeras.

---

### Preview ao vivo
Mostra a imagem atual da câmera selecionada.

Botões:
- `Iniciar`
- `Parar`

---

### Papel da Câmera
Opções observadas:
- Top (Superior)
- Bottom (Inferior)
- Side (Lateral)
- Fiducial
- Desabilitar

---

### Ajustes de Imagem
Sliders/campos para:
- **Foco**
- **Exposição**
- **Brilho**
- **Contraste**
- **Saturação**
- **Balanço Branco**

Botão:
- `Resetar Padrões`

---

### Posição Atual
Mostra coordenadas X Y Z atuais, possivelmente para associar contexto físico à configuração.

### Botões finais
- `Aplicar`
- `Salvar e Fechar`
- `Cancelar`

---

## Significado dos campos de imagem

### Foco
Controla a nitidez da imagem.

### Exposição
Controla o quanto de luz a câmera utiliza para formar a imagem.

### Brilho
Ajusta a intensidade aparente da imagem.

### Contraste
Controla a diferença entre regiões claras e escuras.

### Saturação
Controla intensidade das cores.

### Balanço Branco
Ajusta a correção de cor de acordo com a iluminação.

---

## Fluxo esperado de uso

1. abrir a tela
2. selecionar câmera física
3. iniciar preview
4. escolher o papel lógico da câmera
5. ajustar parâmetros visuais
6. aplicar
7. salvar e fechar

---

## Importância no sistema

Essa tela é essencial para garantir:
- câmera correta em cada papel
- qualidade visual adequada
- consistência entre UI, visão computacional e hardware

---

## Pontos em aberto

- se a configuração é global
- como o sistema lida com duas câmeras do mesmo papel no futuro
- se os ajustes são persistidos por dispositivo ou por papel lógico

---

## Ações relacionadas

- [[acao_abrir_configuracao_cameras|Abrir Configuração de Câmeras]]
- [[acao_iniciar_preview_camera|Iniciar Preview de Câmera]]
- [[acao_salvar_configuracao_camera|Salvar Configuração de Câmera]]

