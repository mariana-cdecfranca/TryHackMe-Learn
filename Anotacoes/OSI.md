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
