# Modelo OSI
- o modelo OSI (Open System Interconnection) fornece uma estrutura padronizada que define como os dispositivos na rede enviam, recebem e interpretam os daods
- dispositivos com diferentes design e funções podem se comunicar com outros dispositivos
- os dados enviados pela rede podem ser compreendidos por outros dispositivos por causa da padronização em camadas (7 camadas)

## Camada 1: Física
- camada corresponde aos componentes físicos do hardware usados em rede
- os dispositivos usam sinais elétricos para transportar dados entre si em sistema binário (0 e 1)
- ex:
   - cabo Ethernet, fibra óptica
 
## Camada 2: enlace de dados (data link)
- garante a comunicação entre os dispositivos na mesma rede através de seus endereçamentos físicos
- dentro de cada dispositvo existe o componente placa de interface de rede **(NIC - Network Interface Card)**, que possui gravado nela fisicamente o endereço MAC
   - o endereço MAC é único e exclusivo de cada dipositivo
 
- quando informações são enviadas pelo rede, o endereço físico é usado para identificar exatamente para onde enviar as informações

## Camada 3: Rede
- na camada de rede é onde acontece o roteamento e a remontagem dos fragmentos de dados
- o roteamento determina o melhor caminho (mais curto/otimizado) para envio dos dados
- tudo é tratado por meio do IP nessa camada
- alguns protocolos determinam qual o caminho ideal e decidem a rota considerando qual caminho é mais curto, confiável (para não ocorrer perda de dados) e
com conexão mais rápida (ex: fibra óptica vs cabo de cobre) 
   - **OSPF (Open Shortest Path First)**
   - **RIP (Routing Information Protocol)**
 
# Camada 4: Transporte
