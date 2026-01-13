# Firewall, VPN e LAN

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
