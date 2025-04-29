### **Capítulo 3: Bitcoin Core**

#### **1. Por que o Bitcoin Core é chamado de "Implementação de Referência"? Quais outras implementações do Bitcoin existem?**
- **Implementação de Referência**: O Bitcoin Core é chamado de "implementação de referência" porque é o software original derivado do código de Satoshi Nakamoto (Bitcoin 0.1, lançado em 2009) e serve como a base para o protocolo Bitcoin. Ele define o comportamento padrão da rede (ex.: regras de consenso, formato de transações) e é mantido pela comunidade de desenvolvedores como o padrão de fato. Antonopoulos destaca que ele é usado para testar e validar outras implementações, garantindo compatibilidade com o protocolo.
- **Outras Implementações**:
  - **Libbitcoin**: Uma implementação em C++ focada em desempenho e modularidade.
  - **btcd**: Escrita em Go, usada para nós completos e carteiras leves, popular entre desenvolvedores Go.
  - **BitcoinJ**: Uma biblioteca Java para clientes leves (SPV), usada em carteiras móveis (ex.: Android).
  - **Bitcoin Knots**: Uma bifurcação do Bitcoin Core com ajustes (ex.: otimizações de desempenho).
  - **Bcoin**: Uma implementação em JavaScript/Node.js, usada para nós completos e carteiras.
- **Nota**: Antonopoulos enfatiza que, apesar da diversidade, o Bitcoin Core domina devido à sua robustez e manutenção contínua.

#### **2. Mais de 95% dos nós Bitcoin rodam Bitcoin Core. Qual é o problema de rodar uma implementação diferente?**
- **Problema de Compatibilidade**:
  - **Risco de Incompatibilidade**: Outras implementações podem interpretar as regras de consenso de forma diferente ou ter bugs, levando a bifurcações acidentais (forks) ou rejeição de blocos/transações pela maioria da rede.
  - **Menor Teste**: O Bitcoin Core é amplamente testado e auditado. Implementações alternativas têm comunidades menores, o que pode resultar em menos revisão e maior chance de erros.
  - **Interoperabilidade**: Algumas implementações podem não suportar todas as funcionalidades do Bitcoin Core (ex.: suporte a novas BIPs), causando problemas de sincronização ou validação.
- **Exemplo**: Se uma implementação alternativa não implementar corretamente uma nova BIP (ex.: SegWit), ela pode rejeitar transações válidas, isolando o nó da rede.
- **Nota de Antonopoulos**: A dominância do Bitcoin Core é uma faca de dois gumes: garante consistência, mas cria um ponto único de falha se houver bugs ou ataques direcionados ao Bitcoin Core.

#### **3. O que são BIPs (Bitcoin Improvement Proposals)? Qual é o papel delas no processo de desenvolvimento do Bitcoin?**
- **Definição**: BIPs (Bitcoin Improvement Proposals) são documentos que propõem melhorias no protocolo, formato de dados, ou comportamento do Bitcoin. Elas são a forma padrão pela qual a comunidade sugere, debate e implementa mudanças.
- **Papel no Desenvolvimento**:
  - **Proposta**: Qualquer pessoa pode submeter uma BIP (ex.: BIP 32 para carteiras HD, BIP 141 para SegWit).
  - **Discussão**: A comunidade (desenvolvedores, mineradores, usuários) debate a proposta em fóruns, listas de e-mails, e repositórios GitHub.
  - **Consenso**: Para ser adotada, uma BIP precisa de consenso amplo. Mudanças no consenso (soft forks ou hard forks) requerem apoio majoritário da rede (ex.: 95% dos mineradores para soft forks como SegWit).
  - **Implementação**: Após aprovação, a BIP é implementada no Bitcoin Core e outras implementações, e os nós atualizam para adotar as novas regras.
- **Exemplo**: BIP 9 (soft fork signaling) define como mineradores sinalizam suporte a mudanças, como a ativação do SegWit.
- **Nota de Antonopoulos**: As BIPs garantem um processo aberto e colaborativo, mas podem ser lentas devido à necessidade de consenso em uma rede descentralizada.

#### **4. Quais são algumas razões comuns para rodar seu próprio nó completo?**
- **Razões Comuns** (Capítulo 3):
  1. **Soberania**: Você valida todas as transações e blocos, sem confiar em terceiros, garantindo que segue as regras do Bitcoin (ex.: evita aceitar transações inválidas).
  2. **Privacidade**: Um nó completo não revela suas transações ou endereços a terceiros (diferente de carteiras SPV, que podem vazar dados para servidores).
  3. **Contribuição à Rede**: Seu nó ajuda a descentralizar o Bitcoin, fornecendo redundância e relay de blocos/transações.
  4. **Desenvolvimento**: Desenvolvedores usam nós completos para testar novas funcionalidades ou BIPs.
  5. **Negócios**: Comerciantes ou exchanges rodam nós para verificar transações em tempo real, sem depender de intermediários.
- **Exemplo**: Um comerciante roda um nó para confirmar pagamentos de clientes diretamente, sem confiar em um serviço de terceiros.
- **Nota de Antonopoulos**: Rodar um nó completo é um ato de autonomia, mas exige recursos (banda larga, armazenamento, ~500 GB para blockchain completa em 2025).

#### **5. Qual é a diferença entre um nó pruned e um nó completo (ou archival)?**
- **Nó Completo (Archival)**:
  - Armazena a blockchain inteira (desde o bloco gênese, 2009), permitindo validar todas as transações históricas.
  - Requer ~500 GB de armazenamento (em 2025, conforme estimativas baseadas no crescimento da blockchain).
  - Ideal para auditorias completas ou fornecer dados históricos a novos nós.
- **Nó Pruned**:
  - Armazena apenas os blocos recentes (ex.: últimos 1 GB ou ~550 MB) e descarta dados históricos após validação.
  - Ainda valida toda a blockchain ao sincronizar, mas não mantém o histórico completo.
  - Requer menos armazenamento (~5-10 GB), mas não pode fornecer dados históricos a outros nós.
- **Nota de Antonopoulos**: Nós pruned são úteis para usuários com recursos limitados (ex.: em laptops), mas sacrificam a capacidade de servir dados históricos, reduzindo a utilidade para a rede.

---

### **Capítulo 4: Keys and Addresses**

#### **1. Qual é a relação entre chaves privadas, chaves públicas e assinaturas?**
- **Chaves Privadas**:
  - Um número secreto (256 bits, gerado aleatoriamente) que permite assinar transações, provando propriedade de BTC.
  - Exemplo: `5K...` (formato WIF, Wallet Import Format).
- **Chaves Públicas**:
  - Derivada da chave privada usando criptografia de curva elíptica (ECDSA, curva secp256k1).
  - Serve para verificar assinaturas e gerar endereços Bitcoin.
  - Exemplo: `04x...` (formato não comprimido) ou `02/03x...` (comprimido).
- **Assinaturas**:
  - Criadas com a chave privada para assinar uma transação, provando que o dono da chave autorizou o gasto.
  - Verificadas pela rede usando a chave pública correspondente, sem revelar a chave privada.
- **Relação**:
  - A chave privada gera a chave pública (via multiplicação de curva elíptica).
  - A chave privada assina transações, produzindo uma assinatura.
  - A chave pública verifica a assinatura, garantindo que a transação é válida.
- **Nota de Antonopoulos**: Essa relação é baseada na assimetria criptográfica: a chave privada é secreta, enquanto a chave pública é compartilhada, garantindo segurança e autenticação.

#### **2. O que é um endereço Bitcoin, e por que endereços são usados em vez de chaves públicas brutas?**
- **Endereço Bitcoin**:
  - Um endereço é uma representação codificada da chave pública (ou script) usada para receber BTC.
  - Exemplo: `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa` (Base58, P2PKH).
  - Gerado a partir da chave pública via hash (RIPEMD160(SHA256(chave pública))) e codificado com Base58Check (para incluir checksum).
- **Por que Endereços em Vez de Chaves Públicas Brutas?**:
  - **Tamanho**: Endereços são mais curtos (26-35 caracteres em Base58) que chaves públicas (130 caracteres não comprimidas, 66 comprimidas), facilitando o uso.
  - **Detecção de Erros**: Endereços usam um checksum (via Base58Check), permitindo detectar erros de digitação.
  - **Segurança**: O hash (SHA256 + RIPEMD160) adiciona uma camada de proteção, tornando mais difícil atacar a chave pública diretamente.
  - **Flexibilidade**: Endereços podem representar scripts complexos (ex.: P2SH), não apenas chaves públicas.
- **Nota de Antonopoulos**: Endereços são uma abstração para facilitar o uso e aumentar a segurança, mas o protocolo subjacente ainda opera com chaves públicas e scripts.

#### **3. Como sabemos que o problema do logaritmo discreto é difícil de quebrar?**
- **Problema do Logaritmo Discreto (DLP)**:
  - No Bitcoin, o DLP é a base da segurança da ECDSA (curva secp256k1): dado um ponto \( P = k \cdot G \) (onde \( G \) é o ponto gerador e \( k \) é a chave privada), é computacionalmente inviável encontrar \( k \) a partir de \( P \) (chave pública).
- **Por que é Difícil?**:
  - **Matemática**: Não existe um algoritmo eficiente para resolver o DLP em curvas elípticas grandes (como secp256k1, com 256 bits).
  - **Teste Empírico**: Décadas de pesquisa em criptografia (desde os anos 1970) não encontraram soluções práticas, mesmo com avanços em computação.
  - **Ataques Conhecidos**: O melhor ataque (Pollard’s Rho) leva tempo exponencial (\( O(\sqrt{n}) \), onde \( n \) é a ordem da curva), ou seja, cerca de \( 2^{128} \) operações para secp256k1, o que é inviável até com supercomputadores modernos.
  - **Computação Quântica**: Algoritmos quânticos (ex.: Shor) podem resolver o DLP em tempo polinomial, mas computadores quânticos capazes disso ainda não existem (em 2025).
- **Nota de Antonopoulos**: A dificuldade do DLP é uma suposição criptográfica amplamente aceita, mas a segurança do Bitcoin depende de avanços futuros não quebrarem essa suposição.

#### **4. O que são scripts de input e output? Como eles se relacionam com o recebimento e gasto de Bitcoins?**
- **Scripts de Output**:
  - Definidos no output de uma transação, especificam as condições para gastar os BTC (ex.: quem pode gastar e como).
  - Exemplo: Em P2PKH, o script de output é `OP_DUP OP_HASH160 <hash do endereço> OP_EQUALVERIFY OP_CHECKSIG`, exigindo que o gastador forneça uma chave pública correspondente e uma assinatura válida.
- **Scripts de Input**:
  - Fornecidos no input de uma transação para desbloquear um output anterior, cumprindo as condições do script de output.
  - Exemplo: Em P2PKH, o script de input é `<assinatura> <chave pública>`, que é verificado contra o script de output para autorizar o gasto.
- **Relação com Recebimento e Gasto**:
  - **Recebimento**: Quando você recebe BTC, o remetente cria um output com um script que "bloqueia" o valor para seu endereço (ex.: P2PKH com seu hash de chave pública).
  - **Gasto**: Para gastar esse BTC, você cria uma transação com um input que fornece um script de input (ex.: sua assinatura e chave pública), desbloqueando o output anterior.
- **Nota de Antonopoulos**: Scripts são o mecanismo de "programação" do Bitcoin, permitindo condições flexíveis para transferência de valor (não apenas "pagar a uma chave").

#### **5. Quais são as diferenças entre P2PKH e P2SH?**
- **P2PKH (Pay-to-Public-Key-Hash)**:
  - O tipo mais comum de transação no Bitcoin.
  - Script de output: `OP_DUP OP_HASH160 <hash da chave pública> OP_EQUALVERIFY OP_CHECKSIG`.
  - O destinatário fornece uma chave pública e uma assinatura no script de input para gastar.
  - Endereço começa com `1` (Base58).
  - Uso: Pagamento direto a um endereço simples (hash de uma chave pública).
- **P2SH (Pay-to-Script-Hash)**:
  - Introduzido pela BIP 16, permite pagar a um script (não apenas a uma chave pública).
  - Script de output: `OP_HASH160 <hash do script> OP_EQUAL`.
  - O gastador fornece o script original (redeem script) e os dados necessários (ex.: assinaturas) no script de input.
  - Endereço começa com `3` (Base58).
  - Uso: Ideal para scripts complexos, como multisig (ex.: 2-de-3 assinaturas) ou contratos.
- **Diferenças**:
  - **Complexidade**: P2PKH é simples (paga a uma chave), P2SH é flexível (paga a um script).
  - **Tamanho e Taxas**: P2SH pode ser mais barato para o remetente (script menor no output), mas mais caro para o gastador (script de input maior).
  - **Segurança**: P2SH esconde a complexidade do script até o gasto, aumentando privacidade.
- **Nota de Antonopoulos**: P2SH foi um passo crucial para transações mais avançadas, como multisig e Lightning Network.

#### **6. O que são endereços Bech32 e Base58? Quais problemas estão associados a cada um?**
- **Base58 (Base58Check)**:
  - Formato tradicional de endereços Bitcoin (usado em P2PKH e P2SH).
  - Exemplo: `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa` (P2PKH), `3EktnHQD7RiAE6uzMj2ZifT9YgRrkSgzQX` (P2SH).
  - Codifica hashes (com checksum) em uma string alfanumérica (exclui caracteres confusos como `0`, `O`, `I`, `l`).
- **Bech32**:
  - Introduzido pela BIP 173 (SegWit), usado para endereços SegWit (P2WPKH, P2WSH).
  - Exemplo: `bc1qw508d6qejxtdg4y5r3zarvary0c5xw7kv8f3t4`.
  - Usa apenas letras minúsculas (a-z) e números (2-7), com um formato mais longo e separado (ex.: `bc1` + hash).
- **Problemas Associados**:
  - **Base58**:
    - **Comprimento Variável**: Difícil de validar visualmente (26-35 caracteres).
    - **Checksum Limitado**: Detecta alguns erros de digitação, mas não todos.
    - **Ineficiência com QR Codes**: Caracteres mistos (maiúsculas e minúsculas) aumentam o tamanho dos QR codes.
    - **Sem Suporte a SegWit**: Não suporta endereços SegWit nativamente, exigindo P2SH como intermediário (mais caro).
  - **Bech32**:
    - **Compatibilidade**: Alguns softwares antigos não suportam Bech32, dificultando a adoção inicial (embora isso tenha diminuído em 2025).
    - **Legibilidade Humana**: Letras minúsculas e formato longo (ex.: `bc1q...`) podem ser menos intuitivos para usuários.
    - **Erro de Digitação**: Embora tenha melhor detecção de erros (código BCH), usuários podem errar ao copiar manualmente.
- **Nota de Antonopoulos**: Bech32 é mais eficiente e seguro (especialmente para SegWit), mas Base58 ainda é amplamente usado por compatibilidade histórica.

---

### **Conexão com Perguntas Anteriores**
- **Inputs e Outputs**: Você perguntou sobre isso para Otthon Leão, e aqui detalhei os **scripts de input e output**, que Antonopoulos explica como o mecanismo para bloquear (receber) e desbloquear (gastar) BTC, conectando diretamente com a transferência de valor.
- **Reversibilidade**: Para Giovanna Vieira, discutimos a irreversibilidade das transações. O Capítulo 3 reforça que a imutabilidade do Bitcoin Core (e sua dominância) é essencial para garantir a segurança e a finalidade das transações, dificultando mudanças como reversibilidade.
