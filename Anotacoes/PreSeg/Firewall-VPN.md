# Firewall, VPN e dispositivos de rede LAN

## Port Forwarding (encaminhamento de portas)
- permite que dispositivos na internet acessem serviços que estão dentro de uma rede interna, privada
   - sem o encaminhamento, os serviços ficariam disponíveis apenas para dispositivos conectados na rede local
(intranet)
   -  para permitir o acesso a serviços de uma rede local por dispositivos na Internet (WAN):
       - utiliza-se um roteador com endereço IP público
       - esse roteador recebe as solicitações vindas da Internet e encaminha o tráfego de entrada para o servidor interno correspondente (IP privado e porta específicos)
       - as respostas do servidor local são automaticamente redirecionadas de volta para a Internet, pois o roteador
mantém o controle das conexões por meio do NAT
       - todo esse processo é configurado no roteador, que utiliza regras para determinar para qual dispositivo
interno cada solicitação externa deve ser encaminhada
    - **Port Forwarding vs Firewall**:
       - port forwarding:
          - encaminha o tráfego, dizendo para onde os pacotes devem ir
       - firewall:
          -  permite ou bloqueia o tráfego, decide se o pacote pode acessar
       - ** mesmo com o port forwarding configurado, o firewall pode bloquear a porta
     
## Firewall
- é um dispositivo na rede responsável por determinar qual tráfego pode entrar e sair
- o firewall analisa cada comunicação com base em critérios como:
   - origem do tráfego
      - ex: pode permitir uma tráfego apenas de uma determinada rede e bloquear algum IP suspeito
   - destino do tráfego
      - ex: pode bloquear acesso interno a servidores internos específicos e permitir acesso a apenas um servidor web
   - porta de destino
     - ex: pode permitir apenas uma porta (80 -> http) e bloquear as outras
   - protocolo utilizado
      - ex: permitir TCP e bloquear UDP ou permitir ambos
    
- para usaar esses critérios, o firewall realiza a inspeção de pacotes:
   - analisa o cabeçalho (informações de IP, porta, protocolo)
   - em firewalls mais avançados, pode inspecionar até o conteúdo dos pacotes
 

### Tipos de firewalls
- hardware dedicado (empresas, data centers)
- roteadores residenciais
- software (ex: Windows Firewall, iptables, Snort)

### Categorias principais de Firewall
- **Stateful (de estado):**
   - utiliza todas as informações de uma conexão e não apenas pacotes individuais
   - determina o comportamento de um dispositivo com base na conexão inteira
   - desvantagens:
      - consome muitos recursos
      - as decisões são dinâmicas (pode permitir as primeiras partes de um handshake TCP e bloquear a conexão inteira
se algo falhar)
   - vantagens:
      - é muito mais seguro e inteligente
    
- **Stateless (sem estado):**
   - usa um conjunto de regras fixas para determinar se um pacote é aceitável ou não
      - ex: se um dispositivo envia um pacote inválido, ele não necessariamente será inteiro bloqueado
   - desvantagens:
      - apesar de usarem menos recursos, são menos eficientes
      - todas as regras precisam ser atendidas para que ele seja útil
   - vantagens:
      - são mais rápidos
      - mais eficientes para lidar com grandes volumes de tráfego (ex: ataques DDoS)


## Noções básicas de VPN (Virtual Private Network)
- permite que dispositivos de redes diferentes se comuniquem de forma segura
   - para isso, um caminho entre eles é criado -> túnel
   - os dispositivos conectados pelo túnel formam sua própria rede privada
 
- permite conexões de redes geograficamente separadas
   - ex: uma empresa com vários escritórios consegue fornecer recursos como servidores/infraestrutura a partir de outro escritório
- oferece privacidade
   - usa criptografia para proteção dos dados
      - os dados enviados só podem ser compreendidos por dispositivos de origem e destino -> inacessíveis a interceptações
- oferece anonimato
   - o tráfego não é visível diretamente pelo provedor de internet
   - o nível de anonimato depende de como os outros dispositivos na rede respeitam a privacidade
 
### Tecnologias VPN
- **PPP (Point-to-Point Protocol):**
   - é um protocolo da camada de enlace usado para estabelecer conexões ponto a ponto
   - é usada pela PPTP para permitir autenticação de criptografia dos dados
   - as VPN's funcionam usando uma chave privada e um certificado público
      - cada dispositivo possui sua própria chave privada e os dois dispositivos trocam certificados públicos -> a conexão é validada pela confiança nos certificados
   - não é roteável -> não consegue sair de uma rede por conta própria -> precisa de um protocolo de tunelamento para virar VPN
 
- **PPTP (Point-to-Point Tunneling Protocol):**
   - permite que os dados do PPP trafeguem e saiam de um rede
   - fácil de configurar e compatível com a maioria dos dispositivos
   - desvantagem: criptografia mais fraca comparando com alternativas, considerada inseguro atualmente
 
- **IPSec (Internet Protocol Security):**
   - criptografa pacotes usando a estrutura do IP
   - é mais difícil de configurar mas oferece criptografia robusta e compatível com muitos dispositivos

## Dispositivos de redes LAN
### Roteador
- é um dispositivo de rede com a função de conectar redes diferentes e encainhar dados entre elas
   - conectar rede de casa com a internet
- roteamento = processo de escolher o melhor caminho para que os dados possam sair de uma rede e chegar na outra
   - identifica o destino do pacote -> consulta tabelas de rota -> encaminha o pacote pelo caminho mais adequado
 
- o roteador opera na camada 3 do modelo OSI (camada de Rede)
   - trabalha com endereços IP e pacotes
 
- normalmente oferecem:
   - interface web ou console
   - configurações de NAT, Port Forwarding
   - firewall
 
- fatores considerados na escolha do melhor caminho:
   - caminho mais curto (menor saltos)
   - caminho mais confiável
   - meio mais rápido (ex: fibra vs cobre)
   - métrica de custo
 
### Switch
- é o dispositivo capaz de conectar vários dispositivos dentro da mesma rede local
   - normalmente conecta de 3 a 63 dispositivos
- usa cabos Ethernet
- atua como **ponto central** da LAN
- **Switch de camada 2:**
   - opera na camada 2 do modelo OSI (enlace)
   - trabalha com frames e endereços MAC
   - aprende os MACs conectados às portas
   - encaminha o frame apenas para a porta correta
 
- **Switch de camada 3:**
   - opera na camada 3 do modelo OSI (rede)
   - encaminha frames, como o switch de camada 2 e encaminha pacotes como um roteador
   - muito usado em redes corporativos ou ambientes com alto tráfego interno

### VLAN (Virtual Local Area Network)
- permite dividir logicamente uma rede física em várias redes virtuais
- mesmo que os dispositivos estejam conectados ao mesmo switch físico, eles podem pertencer a redes diferentes e ser isolados entre si
- vantagens:
   - segurança: setores não se comunicam entre si
   - organização: separação por função
   - controle de tráfego
   - aplicação de regras específicas
 * *a comunicação entre VLAN's só ocorre se um roteador ou um switch de camada 3 permitir isso explicitamente (inter-VLAN routing)
