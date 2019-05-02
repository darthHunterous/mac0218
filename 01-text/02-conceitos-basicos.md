# 02 - Conceitos Básicos de Ruby
* Tudo é objeto
* Símbolos ao final do nome de um método
    * `?`: indica métodos que retornam valores booleanos
    * `!`: altera estado do objeto
* `class`: métodos para saber a classe de um objeto
    * `1729.class`: => `Fixnum`
* `object_id`: retorna a identificação única de um objeto

### 2.1 - Tipos básicos
* Tipos não são declarados
* **Constantes**: variáveis declaradas com uma letra maiúscula no início
    * Valor pode ser mudado, mas gera um warning
<br><br>
* **2.1.1 - Números**
* Inteiros e ponto flutuante
* Divisão de inteiros produz inteiro
* **Bignum**, classe para inteiros muito grandes
* **Exemplo - Imprimir mensagem 10 vezes**
    * `10.times { puts "Já chegamos?" }`
        * `times`: faz com que o bloco à direita seja repetido o número de vezes do inteiro que o chamou
        * Forma econômica de `for`
* Comandos acabam com `final de linha` ou `;`
* `_`: caracter ignorado para legibilidade de números grandes
    * `1_000_000`
<br><br>
* **2.1.2 - Strings**
* Mutáveis e interpoláveis
* Podem ser representadas por `"`, permitindo uso de caracteres como `\n` e `\t`
    * Permite também o uso de interpolação com `#{x}`, sendo o conteúdo entre chaves incluso na string
* `'`: Com aspas simples, a string é literal, sem substituição de caracteres
* `` ` ``: strings representadas por backtick são passadas à **shell**, retornando o resultado da própria shell
* `<<`: usado para identificador o delimitador para encerrar a captura de uma string longa, com várias linhas
    * ```ruby
      longa = <<terminar
      string bem longa
      com varias linhas
      so acaba ao digitar o identificador
      terminar

      # Armazena na variável "longa" a string:
      # "string longa\ncom varias linhas\nso acaba quando digitar o identificador\n"
      ```
* Valores formatados
    * `puts "Produto: %-10.10s\nPreco : %7.2f" %['Acucar', 4.80]`
<br><br>
* **2.1.3 - Símbolos**
* Strings constantes, úteis para serem usadas como chaves ou identificadores
    * `exemplo-simbolo = :chave`
<br><br>
* **2.1.4 - Arrays**
    * Declarar diretamente cada elemento
        * `a = [1, 4, "blah", [1, 3]]`
    * `Array.new(20)`: inicializa com 20 elementos nil
    * `Array.new(3, "bla")`: inicializa com 3 elementos "bla"
    * `Array.new(4) {|x| x*x}`: para cada elemento de índice x, coloca x*x nele
    * `Array(3..5)`: [3, 4, 5]
    * `Array.[](1, 0, 4, "!!")`: [1, 0, 4, "!!"]
    * Inicialização com base em lista de palavras
        * `lista = %w[um dois tres quatro]`: [um, dois, tres, quatro]
<br><br>
* **2.1.5 - Hashes**
    * Dicionários também presentes em Ruby
<br><br>
* **2.1.6 - Ranges (faixas)**
    * Faixas de valores que podem ser usados como índices de `for`, similar a Python
    * Indicados por `(inicio...fim)`, onde fim não está incluso ou `(inicio..fim)`, onde fim está incluso
    * `a = Array(3..6)`: [3, 4, 5, 6]
    * `b = Array('aa'..'cx')`: de "aa" a "az", de "ba" a "bz", e de "ca" a "cx"

### 2.2 - Estruturas de Controle
* **Condicionais - if**
    ```ruby
    if a > 4
        puts "#{a} é maior que quatro"
    end

    # Ou em apenas uma linha
    puts "#{a} é maior que quatro" if a > 4

    # Outra forma inline
    if a > 4 then puts "#{a} é maior que quatro" end
    ```
* **Condicionais - unless**
    * if com condição invertida
    * `puts "#{a} é maior que quatro" unless a <= 4`
* **Switch Case**
    ```ruby
    case a
        when 3 then puts "opa, olha o três aqui"
        when 4 then puts "um pouco maior que três: quatro"
        when 5..10 then puts "vai de cinco a dez"
    end
    ```s
* **While/Until**
    * Similares ao padrão
    * `while` pode ser colocado ao final
        * `puts x -= 1 while x > 0`
            * Com x = 3, irá imprimir 2, 1, 0
* **Controle de laços**
    * `break`: sai do laço atual
    * `redo`: reinicia iteração corrente
    * `retry`: refaz o laço
    * `next`: pula para próxima iteração