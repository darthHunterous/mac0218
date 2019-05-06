# 10 - Exceções e Tratamento de Erros
* **Exceção**: acontecimento inesperado em orientação a objetos
    * Erro ou evento fora do normal, como entrada inválida

### Principais exceções de Ruby
* `NoMemoryError`
* `ScriptError`
    * `LoadError`
    * `NotImplementedError`
    * `SyntaxError`
* `SignalException`
    * `Interrupt`
* `StandardError`
    * `ArgumentError`
    * `IOError`
        * `EOFError`
    * `IndexError`
    * `LocalJumpError`
    * `NameError`
        * `NoMethodError`
    * `RangeError`
        * `FloatDomainError`
    * `RegexpError`
    * `RuntimeError`
    * `SecurityError`
    * `SystemCallError`
    * `SystemStackError`
    * `ThreadError`
    * `TypeError`
    * `ZeroDivisionError`
* Um método pode levantar uma exceção com o comando `raise`
    * A exceção pode ser capturada na pilha de chamadas e ser tratada de acordo ou não ser captura e apresentar-se como mensagem de erro na saída
* **Capturar exceção**: identificação do bloco a ser protegido (análogo a try/catch de outras linguagens)
    * Início do bloco marcado por `begin` e região a tratar o erro com `rescue`
    * **Estrutura**:
        * `begin` seguido pelo código protegido, onde exceções podem ser lançadas
        * `rescue` ou `rescue => e` ou `rescue excecao => e`: ao qual se segue o tratamento da exceção
        * `else`: bloco opcional que segue o tratamento para o caso de exceções não especificadas
        * `ensure`: opcional, seguido por um bloco de código a ser executado sempre, independentemente de ter ocorrido uma exceção
        * `end`
    * `retry` dentro de `rescue` ou `else` faz com que o trecho (desde o begin) seja reexecutado
    ```ruby
    begin
        puts "Entre com um numero negativo"
    # chomp elimina o \n no final
    x = gets.chomp.to_i
    raise "Eu disse negativo" if x >= 0
    puts "Muito bem"
    rescue => e
        # e.message tambem colocado em $
        puts e.message
        retry
    end
    ```

### Várias formas de `raise`
```ruby
# exemplo de RunTimeError
raise RunTimeError.new("mensagem de erro")

# ou 
raise RunTimeError, "Mensagem de erro"

# Para o caso específico de RunTimeError
raise "Mensagem de erro"
```

### Várias formas de `rescue`
```ruby
# pegar qualquer exceção (não recomendável)
rescue

# exceção na variável v, nesse caso, do tipo StandardError
rescue =>v

# para exceção específica
rescue ArgumentError

# ou exceção específica numa variável
rescue ArgumentError => v
```

### 10.1 - `throw` e `catch`
* `catch`: define um bloco com uma *label*, que será terminado se um `throw` for executado para aquela *label*
    * Pulo direto para final de bloco acima na pilha
    * Interrompe o processamento de um aninhamento de chamadas, caindo fora rapidamente (throw e catch é mais rápido que exceções)
```ruby
def Entrada(prompt)
    print prompt
    l = gets.chomp
    throw :refaz if l == "!"

    return l
end

catch :refaz do
    nome = Entrada "Nome: "
    idade = Entrada "Idade: "
    sexo = Entrada "Sexo: "
    puts "Registro completo"
end
```
* `throw` pode especificar o valor de retorno do `catch` com um segundo parâmetro
    ```ruby
    randomNumbers = catch(:randomNumbers) do
        result = []
        10.times do
            num = rand(100)
            throw(:randomNumbers, []) if num % 7 == 0
            result << num
        end
        result
    end

    puts randomNumbers
    ```
    * Garante-se que o vetor não possui múltiplos de 7, pois neste caso será retornado um vetor vazio

