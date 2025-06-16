# Algoritmo de Codificação Base64

## Índice

- [1. Introdução](#1-introdução)
- [2. Desenvolvimento](#2-desenvolvimento)
  - [2.1 Histórico e Origem](#21-histórico-e-origem)
  - [2.2 Funcionamento do Algoritmo](#22-funcionamento-do-algoritmo)
  - [2.3 Aplicações Práticas](#23-aplicações-práticas)
  - [2.4 Tabela Comparativa](#24-tabela-comparativa)
- [3. Exemplo Prático](#3-exemplo-prático)
- [4. Conclusão](#4-conclusão)
- [Referências](#referências)

---

## 1. Introdução

A codificação Base64 é um método amplamente utilizado para representar dados binários como texto ASCII, tornando-os mais seguros e portáveis para transmissões em canais que não suportam diretamente dados binários. Este trabalho apresenta uma visão geral do algoritmo Base64, seu funcionamento, aplicações e exemplos práticos.

## 2. Desenvolvimento

### 2.1 Histórico e Origem

O **Base64** surgiu como uma solução prática no início da expansão da internet e das redes de computadores. Seu desenvolvimento está diretamente associado à necessidade de transmitir dados binários (como imagens, arquivos e anexos) através de sistemas que originalmente foram projetados para trabalhar apenas com texto **ASCII**, como **emails**, **protocolos HTTP** e outros sistemas de comunicação textual.

Nos anos **1980 e 1990**, o **correio eletrônico (email)** se consolidava como uma das principais formas de comunicação digital. Naquela época, os protocolos de envio de emails, como o **SMTP (Simple Mail Transfer Protocol)**, foram projetados para transmitir apenas texto, utilizando o padrão **ASCII de 7 bits**, que não comportava dados binários (como imagens, PDFs ou arquivos executáveis).

#### Surgimento nas Especificações MIME

O algoritmo **Base64** foi formalmente especificado no contexto da padronização de emails com o desenvolvimento do **MIME (Multipurpose Internet Mail Extensions)**, publicado em **1992** sob a **RFC 1521** (posteriormente atualizada para a **RFC 2045**, em **1996**).

O objetivo do MIME era permitir que emails pudessem transportar não só texto, mas também **anexos de qualquer tipo**, como **áudio, vídeo, imagens e arquivos compactados**. O Base64 foi escolhido como um dos métodos para **codificação de dados binários em texto ASCII seguro e legível** para transporte em redes e sistemas que **não eram 8-bit clean** (ou seja, que não suportavam dados fora do ASCII).

#### Como Surgiu o Nome "Base64"

O nome **"Base64"** vem do fato de que o algoritmo trabalha com um conjunto de **64 caracteres distintos**, que são suficientes para representar qualquer dado binário após sua conversão.

### 2.2 Funcionamento do Algoritmo

O algoritmo Base64 opera convertendo dados binários em uma representação textual composta por 64 caracteres do conjunto ASCII. Esse conjunto inclui as letras maiúsculas (A–Z), letras minúsculas (a–z), os números de 0 a 9, e dois caracteres especiais: `+` e `/`. O símbolo `=` é utilizado como caractere de preenchimento quando necessário.

Os **64 caracteres usados são**:

- Letras maiúsculas: `A–Z` (26)
- Letras minúsculas: `a–z` (26)
- Números: `0–9` (10)
- Símbolos: `+` e `/` (2)

Além disso, o caractere `=` é usado como **preenchimento (padding)** para manter a integridade dos blocos de dados.

#### Etapas da Codificação:
1. **Divisão dos Dados:** O fluxo de entrada é dividido em blocos de 3 bytes (24 bits).
2. **Conversão para Grupos de 6 Bits:** Cada bloco de 24 bits é dividido em 4 grupos de 6 bits.
3. **Mapeamento de Caracteres:** Cada grupo de 6 bits é mapeado para um caractere correspondente do conjunto Base64.
4. **Preenchimento:** Se a quantidade de dados não for múltipla de 3, são adicionados um ou dois caracteres `=` para garantir a integridade do bloco final.

![image](https://github.com/user-attachments/assets/d34be3a3-c3c3-496b-a759-822f1bb72a62)

#### Etapas da Decodificação:
1. **Remoção do Preenchimento:** Os caracteres `=` são ignorados.
2. **Conversão Reversa:** Os caracteres Base64 são convertidos de volta para seus valores binários equivalentes.
3. **Agrupamento e Reconstrução:** Os bits são agrupados em blocos de 8 bits (1 byte) e convertidos novamente para a forma original.

### 2.3 Aplicações Práticas

O Base64 é utilizado em várias situações práticas:
- **Redes:** Para codificar dados transmitidos em protocolos como HTTP ou SMTP.
- **E-mails:** Para anexar arquivos binários a mensagens de texto.
- **APIs:** Para transmissão segura de imagens, tokens e dados sensíveis em formato texto.
- **Criptografia:** Na serialização de chaves, certificados e dados criptográficos.
- **Web Development:** Em **Data URIs**, para embutir imagens e outros recursos diretamente em HTML ou CSS.


### 2.4 Tabela Comparativa

| Algoritmo       | Tamanho da Saída | Complexidade | Usado em |
|----------------|------------------|--------------|----------|
| Base64         |  33% maior       | Baixa        | E-mails, APIs |
| Hexadecimal    | 100% maior       | Baixa        | Debug, Logs   |
| Base32         |  60% maior       | Média        | DNS, QR Codes |

## 3. Exemplo Prático

Considerando o exemplo do texto: `Ciência`

### Codificação:

1. **Conversão para UTF-8 (em decimal):**
   - `C` → 67  
   - `i` → 105  
   - `ê` → 195, 170  
   - `n` → 110  
   - `c` → 99  
   - `i` → 105  
   - `a` → 97  

   Resultado: `[67, 105, 195, 170, 110, 99, 105, 97]`

2. **Representação em binário:**
01000011 01101001 11000011 10101010 01101110 01100011 01101001 01100001

3. **Agrupamento em blocos de 6 bits:**
010000 110110 100111 000011 101010 100110 111001 100011 011010 010110 0001

4. **Mapeamento para Base64 (completando bits e aplicando padding):**  
- Blocos em decimal:  
  16, 54, 39, 3, 42, 38, 57, 35, 26, 22, 1  
- Caracteres Base64 correspondentes:  
  `Q`, `2`, `n`, `D`, `q`, `m`, `5`, `j`, `a`, `W`, `E`

**Resultado final em Base64:**
`Q2nDqm5jaWE=`

### Expressão Matemática

A fórmula geral para calcular o tamanho da saída codificada em Base64 é:

Saída_Base64 = 4 × ceil(n / 3)

Onde `n` é o número de bytes da entrada.

## 4. Conclusão

O algoritmo Base64 se destaca como uma solução eficiente para a codificação de dados binários em texto, permitindo sua transmissão e manipulação em sistemas que não operam com dados binários de forma nativa. Embora resulte em um aumento no volume de dados, suas vantagens, como simplicidade, ampla compatibilidade e vasta adoção tornam essa técnica indispensável em diversos contextos da computação moderna, especialmente na troca segura e padronizada de informações.

## Referências

- INSTITUTO MILITAR DE ENGENHARIA. Base64. IMESec Wiki, 2023. Disponível em: https://wiki.imesec.ime.usp.br/books/ctf-starter-pack/page/base64.
- MOZILLA. Base64 - Glossary. MDN Web Docs, 2024. Disponível em: https://developer.mozilla.org/en-US/docs/Glossary/Base64.
- CODEEEEE. Encode Base64. Codeeeee, 2023. Disponível em: https://www.codeeeee.com/pt/encode/base64.html.
- MAYER, Samuel. Explicando Base64. TabNews, 2023. Disponível em: https://www.tabnews.com.br/SamuelMayer/explicando-base64.
- INFRA AS CODE. Base64 não é criptografia. Infra as Code, 2023. Disponível em: https://infraascode.com.br/base64-ne-criptografia/.
