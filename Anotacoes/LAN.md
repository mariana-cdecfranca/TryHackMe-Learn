# Local Area Network (LAN) Topologies
Topologias = projeto / estrutura da rede

## Star Topology (topologia em estrela)
- os dispositivos na rede são conectados a um dispositivo de rede central (normalmente switch)
   - informações são enviadas a um dispositivo conectado através do dispositivo cental 
- modelo mais comum atualmente
  - confiabilidade
  - escalabilidade
- desvantagens
   - se dispositivo central falhar, informações não poderão ser enviadas/recebidas pelos dispositivos conectados
   - quanto mais a rede cresce, maior a necessidade de manutenção
   - exibe cabos e equipamentos dedicados -> mais cara que as outras topologias
 
## Bus Topology (topologia de barramento)
- depende de uma única conexão (backbone cable, cabo de espinha dorsal)
- quando dispositivo envia informação, ela trafega pela espinha dorsal, passando por todos os dispositivos mas somente o disposivo de destino correto aceita e processa os dados
- é mais econômica e mais fácil de configurar
- desvantagem
   - lenta quando dispositivos solicitam dados simultaneamente e propensa a colisões
   - se a espinha dorsal falhar, toda a rede cai
  
## Ring Topology (topologia em anel) 
- os dispositivos conectados formam um anel fechado, de forma que a informação passe de dispositivo em dispositivo, até chegar no destino correto
-  **OBS a topologia em anel com Token Ring, apenas um dispositivo por vez pode transmitir dados, evitando colisões**
-  não depende de um dispositivo central dedicado
-  dados só trafegam em uma direção = manutenção mais simples
-  desvantagens
    - falha em qualquer dispositivo interrompe toda a rede
    - não é eficiente no tráfego, dados passam por muitos dispositivos até chegar ao destino

## Switch
- dispositivos dedicados de rede usados para conectar vários dispositivos na rede Ethernet
   - esses dispositivos são conectados às portas do switch
- podem conectar grande número de dispositivos -> possuem 4, 8, 16, 24, 32 e 64 portas
- mantém o controle de qual dispositivo está conectado em qual porta 
- são mais eficiente que hubs/repetidores -> envia pacote de informação apenas para a porta correta e não para todas, como hubs
   - reduz tráfego de rede
- switches podem ser conectados entre si -> maior redundância, múltiplos caminhos para dados percorrerem = sem inatividade em caso de problemas (se configurado corretamente)

## Roteador
- conecta redes e transmite dados entre elas = **roteamento**
- roteamento = transmissão de dados entre redes, criando caminho entre redes para entrega dos dados
   - escolhe o melhor caminho para enviar dados

# Subnetting (subredes)
- subnetting = divisão de uma rede em subredes menores
   - organização, segurança, controle
   - é obtido dividindo o espaço de endereços IP em partes menores, controlado por um número chamado máscara de sub-rede, que define
     quantos dispositivos (hosts) podem existir em cada sub-rede
- IP: composto por quatro seções, chamadas de octetos
- cada octeto possui 8 bits (0 ou 1)
   - ex: 192.168.1.1
   - em binário
       - 192: 1 1 0 0 0 0 0 0 (128->1, 64->1 32->0, 16->0, 8->0, 4->0, 2->0, 1->0)
       - 168: 1 0 1 0 1 0 0 0 (128->1, 64->0, 32->1, 16->0, 8->1, 4->0, 2->0, 1->0)
       - 1: 0 0 0 0 0 0 0 1 (128->0, 64->0, 32->0, 16->0, 8->0, 4->0, 2->0, 1->1)
       - 1: 0 0 0 0 0 0 0 1 (128->0, 64->0, 32->0, 16->0, 8->0, 4->0, 2->0, 1->1)
- as subredes usam endereços IP para:
   - identificar o endereço de rede: ocorre quando todos os bits da parte de host estão em zero (em redes /24, isso aparece como o último octeto igual a zero)
   - identificar o endereço do host: o host é representado pela parte do IP definida como host pela máscara; cada dispositivo conectado tem o mesmo endereço de rede e endereço de
  host diferente
   - identificar o gateway padrão: endereço especial atribuído a um dispositivo na rede (roteador), que atua como ponto de saída da subrede,
sendo responsável por enviar informações para outras redes (ex: LAN para WAN) 
   - endereço de broadcast: usado para enviar dados a todos os dispositivos da sub-rede;
  ocorre quando todos os bits da parte de host estão em 1 (ex: .255 em redes /24)






