# Fundamentos de Windows - Parte 1
## Sistema de arquivos

- sistema de arquivos = método do sistema operacional para organizar, armazenar, localizar e gerenciar arquivos no disco
- **NFT** = **New Technology File System**
   - é o sistema de arquivos padrão das versões modernas do Windows
   - foi criado para ser mais seguro, confiável e eficiente do que os sistemas anteriores
 
- sistemas de arquivos anteriores do Windows:
   - FAT16 / FAT32 (File Allocation Table):
      - simples e antigo
      - muito compátivel com dispositivos e sistemas
      - FAT32 não suporta arquivos maiores de 4 GB = limitação
      - não possui permissões de segurança nem journaling (arquivo de log com alterações do sistema de arquivos)
      - muito usado em pendrives, cartões SDe sistemas embarcados
      - NÃO é ideial para computadores e servidores modernos
    
   - HPFS (High Performance File System):
      - criado pela IBM para o OS/2
      - uso limitado
      - substituído pelo NTFS no Windows

### NFTS
- é um sistema de arquivos com jounaling
   - mantém um arquivo log (journal) com informações sobre alterações feitas no sistema de arquivos
   - em caso de falha, o NFTS consegue recuperar a estrutura de arquivo automaticamente
   - evite que dados sejam corrompidos de forma grave
 
- suporta arquivos grandes (>4GB)
- possui permissões de segurança
   - controle de acesso por usuário ou grupo -> essencial em ambientes corporativos e servidores
 
- permite compressão de arquivos e pastas = economia de espaço no disco
- Criptografia (EFS – Encrypting File System)
   - protege arquivos com criptografia -> apenas usuário autorizado consegue acessar

#### Permissões no NFTS
- controle total
   - pode ler, escrever, modificar, excluir e alterar permissões
 
- modificar
   - pode alterar e excluir arquivos
 
- ler e executar
   - pode abrir arquivos e executar programas
 
- listar conteúdo da pasta
   - pode ver os arquivos dentro da pasta
 
- ler 
   - apenas visualizar arquivos
 
- escrever
   - criar ou alterar arquivos
 
### Fluxos de Dados Alternativos (ADS – Alternate Data Streams)
- o ADS é um recurso exclusivo do NTFS
- ADS = dados ocultos ligados a um arquivo, mas que normalmente não vemos
   - serve para guardar informações extras associadas a um arquivo sem criar outro arquivo
   - ex: quando baixamos um arquivo da internet, o Windows grava um ADS dizendo que o arquivo veio da internet
   - importância para segurança: um arquivo pode parecer normal mas conter um arquivo malicioso escondido
      - malware pode abusar do ADS -> código malicioso pode ser escondido em um fluxo alternativo
- todo arquivo tem pelo menos um fluxo de dados principal ($DATA)
   - $DATA = o conteúdo normal do arquivo, o qual podemos ver e editar
- o NTFS permite fluxos adicionais escondidos
   - o explorador de arquivos não mostra esses fluxos
   - EX:
      - explorador de arquivo mostra:
         - arquivo.txt
       
      - mas o sistema pode ter:
         - arquivo.txt -> esse aparece
         - arquivo.txt:info -> não aparece
         - arquivo.txt:malware -> não aparece
       

## Pastas Windows\System32
- pasta do Windoes = pasta que contem o sistema operacional
- contém: 
   - arquivos do próprio Windows
   - bibliotecas do sistema
   - drivers
   - ferramentas administrativas
   - configurações essenciais
 
- normalmente fica em C:\Windows, mas não é obrigatório está na unidade C
   - o sistema não depende do nome da unidade, e sim de referências internas -> graças as **variáveis de ambiente**
 ### Variáveis de ambiente
- variáveis de ambiente = servem para o Windows não depender de caminhos fixos
   - guardam informações como:
      - onde o Windows está instalado
      - quantos processadores existem
      - onde ficam pastas temporárias
      - caminhos importantes do sistema
    
   - **%windir%**
      - é uma variável de ambiente do sistema que aponta para a pasta onde o Windows está instalado
      - normalmente: %windir% = C:\Windows
    
## Estrutura da pasta Windows
- algumas subpastas comuns:
   -  Temp: arquivos temporários
   -  Fonts: fontes do sistema
   -  Logs: registros do sistema
   -  WinSxS: componentes do Windows
   -  System 32: arquivos essenciais para o funcionamento do Windows
 
### Pasta System32
- contém arquivos essenciais para o funcionamento do Windows
   - executáveis do sistema (.exe)
   - bibliotecas (.dll)
   - ferramentas administrativas
   - comandos usados no Prompt e PowerShell
   - ex: cmd.exe | powershell.exe| taskmgr.exe | services.msc
 
- muitos serviços usam esses executáveis
- se um arquivo importante for apagado ou alterado:
   - o sistema pode não inicializar
   - serviços param de funcionar
   - Windows pode ficar inutilizável
 
- **em sistemas Windows 64 bits, a pasta ainda se chama System32 por compatibilidade com softwares antigos**

## Tipos de contas de usuário
- em um sistema Windows local (ou seja, não é domínio), existem dois tipos de conta:
   - administrador:
      - é a conta com controle total do sistema, responsável por gerenciar o computador
      - pode:
         - criar, remover e modificar usuários
         - alterar grupos
         - mudar configurações do sistema
         - instalar e remover programas
         - acessar áreas protegidas do sistema
       
   - usuário padrão:
      - conta com permissões limitadas -> evita que qualquer usuário quebre o sistema
      - pode:
         - criar e alterar arquivos apenas nas próprias pastas
         - usar programas já instalados
      - não pode:
         - instalar programas
         - alterar configurações do sistema
         - criar ou remover usuários
         - modificar grupos
       
- cada usuário possui um perfil em C:\Users
- o perfil é criado no primeiro login
- usuários herdam permissões dos grupos aos quais pertencem
- o gerenciamento pode ser feito via Configurações ou lusrmgr.msc

## Controle de conta de usuário
- a maioria dos usuários domésticos usa conta Administrador local, faz tudo logado como administrador
   - problema: administrador pode alterar o sistema inteiro
      - se algo malicioso rodar nessa conta:
         - pode instalar programas
         - alterar arquivos do sistema
         - criar usuários
         - desativar segurança
       

### UAC (User Account Control)
- a Microsoft criou o Controle de Conta de Usuário (UAC) para reduzir essa risco
   - introduzido no Windows Vista
   - mantido em todas as versões seguintes do Windows
 
- mesmo que você esteja logado como administrador:
   - sua sessão NÃO roda o tempo todo com privilégios elevados -> trabalha como usuário comum
   - só vira “superusuário” quando realmente precisa, quando ação exige privilégios elevados -> UAC pede confirmação
 
- o UAC não se aplica (por padrão) à:
   - conta de administrador local integrada (built-in Administrator)
   - essa conta já roda tudo com privilégio máximo o tempo todo
 
- um ícone com escudo indica uso de UAC

## Alterações no sistema
- existem dois locais principais para alterar configurações do sistema:
   - configurações
   - painel de controle
 

### Painel de controle
- por muitos anos foi o principal local para:
   - adicionar ou remover programas
   - adicionar impressoras
   - configurar rede
   - ajustar hardware
   - alterar contas de usuário
     
- é mais técnico e oferece configurações mais detalhadas e avançadas

### Menu configurações
- foi introduzido no Windows 8, que foi pensado para: tablets e telas sensíveis ao toque
   - depois disso: continuou no Windows 10 e tornou-se o local principal para alterações comuns
- oferece:
   - interface mais simples
   - ícones grandes
   - organização mais amigável
   - é o menu preferido para usuários comuns

- algumas opções ainda dependem do painel de controle
- em certos casos, menu configurações redireciona para o painel de controle
- a busca do menu iniciar é a forma mais rápida de encontrar configurações

## Gerenciador de tarefas
- é uma ferramenta do Windows que mostra:
   - plicativos em execução
   - processos do sistema
   - uso de CPU
   - uso de Memória (RAM)
   - uso de Disco
   - uso de Rede
- ajuda a monitorar o sistema, diagnosticar problemas e encerrar programas travados
- usar: ctrl + shift + esc
- é fundamental para:
   - identificar processos desconhecidos
   - ver programas rodando sem autorização
   - analisar comportamento anormal do sistema
   - apoiar análise básica de incidentes
 
### Visualização
- modo simples → visão geral rápida
- mais detalhes → visão completa do sistema
- aba Processos → o que está rodando
- aba Desempenho → como o hardware está sendo usado


# Fundamentos de Windows - Parte 2
## Configurações do sistema
- system configuration -> **MSConfig**
   - é uma ferramenta de solução de problemas avançada, usada principalmente para:
      - diagnosticar problemas de inicialização
      - controlar o que o Windows carrega no boot
      - analisar serviços e opções de inicialização
- não é uma ferramenta para uso diário, e sim para troubleshooting
- requer privilégios de administrador local para ser aberta
- aba:
   - general:
      - define o que o Windows carrega durante a inicialização
    
   - boot:
      - permite configurar opções avançadas de boot, como:
         - modo de inicialização
         - opções de depuração
         - configurações usadas para troubleshooting
      - muito usada quando sistema tem dificuldade para iniciar
    
   - service:
      - mostra todos os serviços do sistema, estejam eles em execução ou parados
      - *serviço = tipo especial de programa que:
      - roda em segundo plano
      - geralmente inicia junto com o Windows
      - não depende de interação do usuário
      - é possível identificar serviços problemáticos
    
   - startup:
      - *existe uma diferença importante entre Windows cliente e Windows Server
         - em Windows 10 / 11:
            - MSConfig não gerencia mais programas de inicialização
            - a Microsoft recomenda usar o gerenciador de tarefas
          
         - em Windows Server:
            - não existe aba startup no gerenciador de tarefas
            - a aba Startup do MSConfig também não mostra nada útil
          
         - em servidores:
            - programas de inicialização do usuário ficam na Startup Folder
          
      - tools:
         - lista várias ferramentas administrativas do Windows, com descrição de cada uma
       
### Configurações avançadas
- oferece configurações avançadas para:
   - desempenho
   - memória
   - recuperação do sistema
 
### Memória virtual (page file)
- O Windows usa um page file como memória virtual quando a RAM física se esgota
- ajuda a:
   - evitar travamentos
   - evitar crashes de aplicativos
   - manter o sistema funcionando sob carga
 
### Inicialização e recuperação
- Windows pode gerar um crash dump quando ocorre um erro crítico, como a Blue Screen of Death (BSOD)
- crash dump serve:
   - análise de falhas
   - diagnóstico técnico
   - investigação de problemas graves

## Configurações do UAC
