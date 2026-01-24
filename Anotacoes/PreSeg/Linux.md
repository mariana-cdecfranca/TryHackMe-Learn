# Fundamentos de Linux
## Comandos básicos

- **echo:** exibe qualquer texto que quisermos
  - Obs.: para que um texto com mais de uma palavra seja tratado como **um único argumento**, ou para
**preservar espaços**, é necessário usar aspas "", pois espaços mudam a forma como o shell interpreta os argumentos
- **whoami:** mostra qual usuário está conectado

## Interagindo com sistema de arquivos
- **cd (change directory):** muda de diretório
- **ls (listing):** lista todo o conteúdo no diretório atual
- **cat (concatenating):** concatena arquivos e exibe conteúdo
- **pwd (print working directory):** imprime o diretório atual

## Procurando arquivos
- **find:** usado para procurar arquivos e diretórios no sistema
   - ex1: busca por nome
      - **find -name log.txt** ou **find /home -name log.txt**
   - ex2: busca por tipo (f -> arquivo e d-> diretório)
      - **find -type f** ou **find -type d**
   - ex3: busca por extensão
      - **find -name "*.txt"**
   - ex4: busca por tamanho
      - **find -size +10M**
    
- **grep (global regular expression print):** usado para encontrar padrões de texto dentro de arquivos
   - ex:  **grep 1234 arquivo.txt**
 
- **wc:** usado para contar linhas, palavras e bytes/caracteres
   - saída padrão: linhas palavras bytes nome_do_arquivo
   - opções (flags):
      - -l linhas | -w palavras | -c bytes | -m caracteres
    

## Operadores
- operador &:
   - usado para executar um comando em segundo plano
      - **firefox &** -> o terminal deve ficar desocupado logo após a execução desse comando, enquanto abre o navegador
 
- operador &&:
   - permite executar vários comando em uma única linha do terminal **(apenas se o primeiro for bem sucedido)**
   - ex:
      - **comando1&&comando2** 
 
- operador >:
   - permite direcionar a saída de um comando para um arquivo
   -  exs:
       - **ls > teste.txt**
       - echo teste > arquivo_exemplo
       - **obs:** caso o arquivo exista, ele será **sobrescrito**
    
- operador >>:
   - também permite direcionar a saída de um comando para um arquivo mas ao invés de sobrescrever o arquivo,
o conteúdo é adicionado ao final **(concatena)**

## SSH (Secure Shell)
- permite executar comandos remotamente em outro dispositivo
- estabelece conexão criptografada entre dispositivos
   - todos os dados enviados entre os dispositivos são criptografados quando transmitidos por uma rede como a internet
 
### Conectando
- sintaxe para conexão:
   - *ssh usuario@ip_do_servidor_remoto*

## Flags e Switches
- os argumentos usados nos comandos identificados por um hífen e uma palavra-chave específica são conhecidos como flags ou switches
   - ex: *ls -a* ou *ls --all* -> esse comando lista também arquivos/pastas ocultos, identificados por "."
 
- o comando *man* fornece a documentação do comando
   - ex: *man ls*
 
## Interação com o sistema de arquivos
- **touch:** cria um arquivo
- **mkdir (make directory):** cria uma pasta
- **cp (copy):** copia um arquivo ou pasta
   - ex:
      - *cp nota1 nota2* -> copia conteúdo de nota1 para nota2
- **mv (move):** mover um arquivo ou pasta
   - além de mover, esse comando também pode renomear um arquivo
      - ex:
         - *mv nota1 nota2* -> agora *nota1* foi renomeado para nota2
- **rm (remove):** remover um arquivo ou pasta
   - ex:
      - *rm teste.txt* -> arquivo pode ser removido
      - *rm -R minhapasta* -> usar *-R* para remover uma pasta
- **file:** determina o tipo de arquivo
- 
