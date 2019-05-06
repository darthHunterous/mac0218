# 11 - Metaprogramação
* Possibilidade de extensão do código em tempo de execução
* Ruby é capaz de **introspecção** por ser linguagem de script interpretada
* **Introspecção**: o programa tem acesso à própria estrutura de dados, sendo possívle criar código dinamicamente com métodos especiais e recursos sintáticos
* **Blocos** podem ser injetados em outras funções
* **Blocos**, `procs` e `lambdas` são **closures**, capturando o escopo do momento de sua criação
    * Permite criar funções que geram funções
* Recurso que ajuda a faze metaprogramação:
```ruby
def mold(base, tam)
    lin = base*tam
    res = lamba { |x|
        puts lin
        yield x
        puts lin
    }
end

f = mold("-", 12) {p "oi"}
f.call(90)
g = mold("=", 45) {|x| p x*50}
g.call(90)
```

### 11.1 - Introspecção
* Cerne da metaprogramação: capacidade de observar a própria estrutura
* Método para consultar se um objeto responde a um dado método
    ```ruby
    42.respond_to? :times  # true
    42.respond_to? :odd?  # true
    42.respond_to? :nome_inventado  # false
    ```
* Hierarquia de classes e métodos
    ```ruby
    String.ancestors  # [String, Comparable, Object, Kernel, BasicObject]
    42.class  # Fixnum
    Integer.superclass  # Numeric
    ```
* Verificar métodos e atributos
    ```ruby
    Strings.methods
    42.methods
    Integer.superclass

    class Algo
        def initialize(n)
            @v = n
            @outra = 0
        end
    end
    x = Algo.new(2)
    x.instance_variables  # [:@v, :@outra]
    ```
* Toda chamada de método é uma mensagem ao objeto dizendo o que deve ser feito
    ```ruby
    class C
        def grite
            puts "AAAAARRRGHYOOOWWWLLL"
        end
    end

    c = C.new
    c.grite  # executa
    c.send "grite"  # executa
    c.send :grite  # executa
    g = "grite"
    c.send(g)  # executa
    # ou c. send g
    ```
    * No exemplo acima, o método `grite` é executao quatro vezes

### 11.2 - Classes Abertas
* Como as classes são abertas, pode-se mexer na implementação a qualquer momento
```ruby
class Array  # classe padrão
    def nao
        puts "Não é possível"
    end
end

[].nao
```
* Não se trata de herança, mas alteração da própria classe

### 11.2.1 - Objetos Abertos
* Ao criar uma instância, ela ganha uma classe adicional exclusiva dela (**singleton**), inserida, na hierarquia, entre a instância e a classe mãe
    * Tal classe pode ser alterada
    ```ruby
    class A
    end

    a = A.new
    b = A.new

    def b.oi
        puts "oi"
    end

    a.oi  # não definido
    b.oi  # imprime "oi"
    ```
* Também permite-se que um bloco seja executado dentro do escopo de uma instância ou classe, tendo acesso ao estado interno, podendo modificar a classe ou instância a ser executada
    * Em vez de bloco de código, tambem pode-se passar uma string com o código a ser interpretado
    ```ruby
    class A
        def initialize
            @num = 42
        end
        def num
            @num
        end
    end

    a = A.new
    a.instance_eval { puts 2*num }
    a.instance_eval { puts 2*@num }
    a.instance_eval "puts 2*num"
    a.instance_eval "def uia ; puts 'caramba' ; end"
    a.uia  # imprime "caramba"
    ```
    * De maneira análoga, `class_eval` executa o bloco no escopo da classe, sendo vísivel a todas instâncias
    * `eval` com interpretação de strings pode levar a falhas de segurança

### 11.3 - Criação dinâmica de métodos
* Forma mais compacta de se criar métodos para uma classe ou instância: `define_method`, método privado
```ruby
class A
    # forma alternativa de definição de método
    define_method(:ok) {puts "normal"}

    # criação dinâmica
    def cria(s)
        # self.class.define_method(s) para generalizar
        A.define_method(s) {puts "eu sou #{s}"}
    end
end

a = A.new
a.ok
a.cria("oi")
a.oi
```
* No exemplo acima, `cria` está amarrada à classe A, ruim para herança, uma solução seria substituir `A` por `self.class`
* Há também o método `define_singleton_method` de comportamento similar ao método análogo
* `method_missing` chamado toda vez que um método não é encontrado, recebe como parâmetros: nome do método, argumentos passados e o bloco
* `send`: delega para outra classe ou objeto que implementará o método faltante