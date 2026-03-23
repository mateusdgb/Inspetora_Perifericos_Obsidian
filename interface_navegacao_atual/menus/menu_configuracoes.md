# Menu: Configurações

## Objetivo

O menu **Configurações** centraliza parâmetros gerais de operação da aplicação e da célula de inspeção.

Ele reúne opções que afetam:

- aparência da interface
- modo real ou simulado
- mapeamento e papel das câmeras
- comunicação com CLP
- cadastro e parametrização de bandejas

---

## Itens observados

- **Tema**
- **Simulação**
- **Configurar Câmeras...**
- **Conexão CLP...**
- **Cadastro de Bandejas...**

---

## Explicação conceitual de cada item

### Tema
Permite alterar a aparência visual do sistema.

Pelos prints, existem:
- Auto (detectar do sistema)
- Claro
- Escuro

Isso afeta a experiência de uso e a legibilidade da interface.

---

### Simulação
Permite operar o sistema em **modo simulado**, sem depender do hardware físico real.

O modo simulado é útil para:
- desenvolvimento
- testes preliminares
- validação de UI
- treinamento

---

### Configurar Câmeras
Permite:
- escolher qual dispositivo físico será usado
- definir o papel lógico de cada câmera
- ajustar parâmetros de imagem

Papéis observados:
- Top (Superior)
- Bottom (Inferior)
- Side (Lateral)
- Fiducial
- Desabilitar

Ajustes observados:
- Foco
- Exposição
- Brilho
- Contraste
- Saturação
- Balanço de Branco

---

### Conexão CLP
Permite configurar a comunicação com o CLP:
- endereço IP
- porta Modbus
- timeout
- teste de comunicação
- conexão/desconexão
- log

---

### Cadastro de Bandejas
Permite cadastrar e editar bandejas da máquina.

Tipos observados:
- Entrada
- Saída OK
- Saída NG
- Universal

Também permite configurar:
- grid da bandeja
- espaçamento
- posição de referência
- abertura/fechamento de garra
- validação por fiduciais

---

## Documentos relacionados

- [[dialogo_configuracao_tema|Configuração de Tema]]
- [[dialogo_configuracao_simulacao|Configuração de Simulação]]
- [[dialogo_configuracao_cameras|Configuração de Câmeras]]
- [[dialogo_configuracao_clp|Configuração de Conexão CLP]]
- [[dialogo_cadastro_bandejas|Cadastro de Bandejas]]