# Modelo OSI
- o modelo OSI (Open System Interconnection) fornece uma estrutura padronizada que define como os dispositivos na rede enviam, recebem e interpretam os daods
- dispositivos com diferentes design e funções podem se comunicar com outros dispositivos
- os dados enviados pela rede podem ser compreendidos por outros dispositivos por causa da padronização em camadas (7 camadas)

## Camada 1: Física
- camada corresponde aos componentes físicos do hardware usados em rede
- os dados são transmitidos como sinais elétricos, ópticos ou de rádio, representados em bits (0 e 1)
- ex:
   - cabo Ethernet, fibra óptica, onda de rádio
 
## Camada 2: Enlace de dados (data link)
- garante a comunicação entre os dispositivos na mesma rede através de seus endereçamentos físicos
- dentro de cada dispositvo existe o componente placa de interface de rede **(NIC - Network Interface Card)**, que possui gravado nela fisicamente o endereço MAC
   - o endereço MAC é único e exclusivo de cada dipositivo
 
- quando informações são enviadas pelo rede, o endereço físico é usado para identificar exatamente para onde enviar as informações
- garante que os dados cheguem ao próximo dispositivo local (próximo salto)
- **OBS:** a camada 2 atua em cada rede local do caminho, inclusive entre roteadores

## Camada 3: Rede
- é responsável pelo endereçamento lógico e roteamento
- o roteamento determina o melhor caminho (mais curto/otimizado) para envio dos dados
- tudo é tratado por meio do IP nessa camada
- alguns protocolos determinam qual o caminho ideal e decidem a rota considerando qual caminho é mais curto, confiável (para não ocorrer perda de dados) e
com conexão mais rápida (ex: fibra óptica vs cabo de cobre) 
   - **OSPF (Open Shortest Path First)**
   - **RIP (Routing Information Protocol)**
 
- não garante entrega nem ordem dos dados, apenas **encaminha**
 
## Camada 4: Transporte
- responsável pela comunicação de ponto a ponto entre os dispositivos
- trabalha com portas, segmentação (fragmentar os em partes menores dados) e remontagem
- define qual aplicação deve receber os dados de destino
- principais protocolos: TCP e UDP
- TCP (Transmission Control Protocol):
   - orientado à conexão  
   - construído com foco na confiabilidade e garantia
   - mantém a conexão entre dois dispositivos durante todo o processo de envio/recebimento de dados
   - garante que os fragmentos de dados enviados na camada de sessão sejam recebidos e remontados na mesma ordem
   - vantagens/desvantagens:
      - garante precisão dos dados / requer conexão confiável entre os dispositivos (se uma parte não for recebida,
o restante não poderá ser utilizado)
      - sincroniza dispositivos e evita que um seja inundado de dados do outro / conexão lenta pode causar gargalos em outro dispositivo, pois a conexão fica reservada no computador receptor durante o tempo todo
      - executa muito mais processos para garantir confiabilidade / muito mais lento que o protocolo UDP   
   - usado em casos de compartilhamento de arquivos, navegação na internet e envio de e-mails (situações que exigem que os dados sejam precisos e completos)  
- UDP (User Datagram Protocol):
   - não orientado à conexão
   - não possui recursos de verificação de erros e confiabilidade como o TCP
   - os dados são enviados, independentemente de chegarem ao destino ou não
   - não há sincronização entre os dispositivos
   - vantagens/desvantagens:
      - muito mais rápido / não importa se dados chegaram ou não
      - deixa a decisão de controle de velocidade de envio na camada de aplicação / oferece flexibiidade aos desenvolvedores de software
      - não mantém conexão contínua entre os dispositivos / conexão instáveis são ruins para usuário
   - são úteis onde pequenos fragmentos de dados são enviados, ou arquivos maiores como vídeos de streaming (não há problema em partes do vídeo pixelizadas)
 
## Camada 5: Sessão
- é responsável por estabelecer (inicia a comunicação), gerenciar (define quem pode transmitir em determinado momento), sincronizar (insere pontos de vericação ou checkpoints, garantindo a retomada da sessão a partir do último ponto válido caso a conexão caia, sem precisar reiniciar tudo) e encerrar a comunicação entre dispositivos se comunicando pela rede
- as sessões são únicas, então dados não podem trasitar entre sessões diferentes

## Camada 6: Apresentação
- atua como um tradutor entre a camada de aplicação e o computador receptor
   - converte os dados em um formato comum entre sistemas diferentes, garantindo que sejam corretamente interpretados
      - sistema Linux enviando dados para sistema Windows
   - garante confidencialidade, criptografando os dados antes de enviar e descriptografando ao receber
      - ex: protocolo HTTPS ao visitar site seguro
    
## Camada 7: Aplicação
- é a camada mais próxima do usuário do ponto de vista lógico
- fornece protocolos de aplicação que permitem que os programas utilizem serviços de rede e se comuniquem pela rede
- OBS: não é a aplicação em si, mas a interface lógica de acesso à rede
   - ex de aplicações do usuário: navegador, serviços de e-mails
   - ex de protocolos: HTTP, HTTPS, DNS

## Resumo
- Camada 7: aplicação - 🖥️
- Camada 6: apresentação - ABC → ### | 🔒 → 🔓
- Camada 5: sessão -  💬 ↔ 💬
- Camada 4: transporte - 🍕 | TCP / UDP | 🚪
- Camada 3: rede - 🌐 🕸️ 🧭 | 📦 IP
- Camada 2: enlace de dados -  📦 → ✉️ + MAC
- Camada 1: física - ⚡ → 0101                               

# Frames e Packets
- são unidades de dados que transportam partes de uma informação/mensagem maior

- **packet:** é um conjunto de dados da camada 3 (rede) que possui informações como endereço IP de origem, endereço IP de destino e carga útil (payload)
- **frame:** é utilizado na camada 2 (enlace), encapsula o pacote e adiciona informações complementares, como **endereço MAC** de origem e destino
- cabeçalhos comuns que os pacotes podem carregar (dependendo da camada):

| cabeçalho | função |
|----------|----------|
| Time to life  | define o número máximo de saltos que um pacote pode dar na rede, evitando loops e sobrecarga caso não chegue ao host  |
| CheckSum | verifica a integridade dos dados na camada em que está definido (IP ou TCP); se os valores forem diferentes, os dados são considerados corrompidos |
| Source Address | endereço de origem (IP ou MAC, dependendo da camada) de onde o pacote é enviado |
| Destination Address | endereço de destino (IP ou MAC, dependendo da camada) para onde o pacote deve ser enviado |


## Protocolo TCP/IP e Three-way handshake
- o protocolo TCP/IP consiste em 4 camadas:
   - aplicação
   - transporte
   - internet
   - interface de rede
 
- o TCP, dentro da pilha TCP/IP, é baseado em conexão: estabelece conexão entre um cliente e o dispositivo servidor antes que os dados sejam enviados
- os pacotes TCP contém várias informações (pacotes):
   -  porta de origem: geralmente é uma porta efêmera (dinâmica, temporária), normalmente acima de 1024, disponível no momento da conexão
       - valor escolhido aleatoriamente entre as portas 0 e 65535 que esteja dnão estejam em uso no momento
    
   -  porta de destino: valor representa o número da porta que o aplicativo/serviço está sendo executado no host remoto
       - valor não é escolhido aleatoriamente 
       - ex: servidor web em execução na porta 80
    
   -  IP de origem: endereço IP do dispositivo que está enviando o segmento
   -  IP de destino: endereço IP do disposivo que está recebendo segmento
   -  número de sequência: identifica a ordem dos dados enviados; o primeiro valor é gerado de forma aleatória no início da conexão 
   -  número de confirmação (ACK): indica o próximo byte esperado pelo receptor
   -  soma de verificação: garante a integridade do segmento TCP por meio de um cálculo matemático; se o valor não corresponder, o segmento é descartado
   -  flag: determina como o segmento deve ser tratado durante o estabelecimento, manutenção ou encerramento da conexão
 
### Three-way handshake
- etapa 1 - **SYN**: mensagem SYN é o pacote inicial enviado durante o handshake, é usado para conectar e sincronizar dispositivos
- etapa 2 - **SYN/ACK**: pacote enviado pelo receptor (servidor) para confirmar a tentativa de sincronização
- etapa 3 - **ACK**: pacote de confirmação, pode ser enviado tanto pelo cliente quanto pelo servidor

após essas três etapas, a conexão TCP está estabelecida

- **DATA**: transmissão de dados ocorre após o handshake
- **FIN**: encerramento controlado da conexão
- **RST**: encerra a conexão de forma abrupta quando ocorre erro ou problema na comunicação

## Protocolo UDP/IP
- não exige conexão entre os dispositivos
- não há confirmação de recebimento, ordenação ou retransmissão de dados, portanto, **não ocorre o Handshake**

## Portas
- número que varia entre 0 e 65535
- cada porta indica qual serviço/aplicativo está se comunicando
- quando um dispositivo envia ou recebe dados, esses dados passam por uma porta
- para evitar confusão, cada serviço normalmente escuta uma porta padrão
   - ex: web = porta 80 (HTTP) | web segura = 443 (HTTPS)
      - dessa forma, os navegadores interpretam os dados da forma forma, mudando apenas a interface (Chrome, Mozilla, etc)
    
   - protocolos que possuem regras padrão:
 
| Protocolo | Porta | Descrição |
|---------|------|-----------|
| FTP (File Transfer Protocol) | 21 | Protocolo utilizado para transferência de arquivos em um modelo cliente-servidor. |
| SSH (Secure Shell) | 22 | Protocolo usado para acesso remoto seguro a sistemas por meio de interface de texto. |
| HTTP (Hypertext Transfer Protocol) | 80 | Protocolo responsável pela comunicação da World Wide Web, usado para transferir páginas, imagens e vídeos. |
| HTTPS (Hypertext Transfer Protocol Secure) | 443 | Versão segura do HTTP, que utiliza criptografia para proteger os dados transmitidos. |
| SMB (Server Message Block) | 445 | Protocolo para compartilhamento de arquivos, pastas e dispositivos como impressoras em rede. |
| RDP (Remote Desktop Protocol) | 3389 | Protocolo que permite acesso remoto a um computador por meio de interface gráfica. |
