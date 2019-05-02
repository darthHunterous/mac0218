# 03 - Funções, Blocos, Procedimentos e Lambdas
* **Definição de Função**: similar a Python
    ```ruby
    def quadrado(x)
        return x*x
    end
    # Não é necessário o ":" ao final da primeira linha
    ```
* **Bloco:** trecho de código que pode receber parâmetros
    * Delimitado por **chaves** ou **do/end**
    * Não tem nome
    * Não pode ser salvo em variável para referência futura
    * Funciona como estrutura sintática
    * Não verificam o número de argumentos
* `yield()`: chama o bloco que foi passado como argumento de uma função