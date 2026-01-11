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
