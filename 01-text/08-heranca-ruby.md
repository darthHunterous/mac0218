# 08 - Herança em Ruby
* Classe que define uma **Progressão** genérica
    ```ruby
    #!/usr/bin/env ruby
    # coding: utf-8

    class Progressao
        def initialize(ini=0)
            @prim = ini
            @atual = ini
        end

        def primeiro
            @atual = @prim
        end

        def prox
            atual += 1
        end

        def imprime(n=1)
            print "#{@prim}"
            for i in 2..n
                print "#{prox}"
            end
        end
    end
    ```
* **`require`**: Faz que um código contido em um arquivo `.rb` seja lido e processado
    * **Progressão Aritmética**:
    ```ruby
    #!/usr/bin/env ruby
    # coding: utf-8

    require "./Progressao"

    class Aritmetica < Progressao
        def initialize(inc=1, ini)
            @inc = inc
            super(ini)
        end

        def prox
            @atual += @inc
        end
    end
    ```
    * **Progressão Geométrica**:
    ```ruby
    #!/usr/bin/env ruby
    # coding: utf-8

    require "./Progressao"

    class Geometrica < Progressao
        def initialize(inc=1, ini)
            @inc = inc
            super(ini)
        end

        def prox
            @atual *= @inc
        end
    end
    ```
    * **Progressão de Fibonacci**
    ```ruby
    #!/usr/bin/env ruby
    # coding: utf-8

    require "./Progressao"

    class Fibonacci < Progressao
        def initialize(v1=0, v2=1)
            @ant = v1
            @atu = v2
            super(v2)
        end

        def prox
            @ant, @atu = @atu, @atu + @ant
            return @atu
        end
    end
    ```
    * **Exemplo de uso**:
    ```ruby
    #!/usr/bin/env ruby
    # coding: utf-8

    require "./Arit"
    require "./Geom"
    require "./Fibo"

    a = Aritmetica.new(2,7)
    g = Geometrica.new(4,5)
    f = Fibonacci.new(1,1)

    def linha() puts "\n" + "-"*20; end

    a.imprime(20)
    linha
    g.imprime(4)
    linha
    f.imprime(5)
    linha
    ```

