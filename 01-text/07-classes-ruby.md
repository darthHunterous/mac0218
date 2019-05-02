# 07 - Classes em Ruby
* Convenção: nomes de classes começando com letra maiúscula
```ruby
#!/usr/bin/env ruby
# coding: utf-8
class Carta
    def initialize(n, v)
        @naipe = n
        @valor = v
    end
    def to_s # to_string, talvez to_s seja padrão do Ruby
        "%2s de %s"%[@valor, @naipe]
    end
end

class Baralho
    def initialize
        @cartas = []
        %w[C, H, S, G].each do |n|
            (["A"] + Array(2..10) + ["J", "Q", "K"]).each do |v|
                @cartas << Carta.new(n, v)
            end
        end
    end

    def print
        @cartas.each do |c| puts c; end
    end

    def embaralha
        emb = []
        while @cartas.size > 0
            i = rand(0 ... @cartas.size)
            emb << @cartas.delete_at(i)
        end
        @cartas = emb
    end

    def distribui(numOfPlayers, numOfCardsPerPlayer)
        return nil if numOfPlayers * numOfCardsPerPlayer > @cartas.size

        playersHands = Array.new(numOfPlayers)
        playersHands.map! {|p| p = Array.new }

        (1..numOfCardsPerPlayer).each do |i|
            (0..numOfPlayers).each do |j|
                playersHands[j] << @cartas.pop
            end
        end
        
        return playersHands
    end
end

b = Baralho.new
b.embaralha
b.print
print("----" * 5)
puts
m = b.distribui(3, 2)

(0...m.size).each do |i|
    puts "Cartas do jogador n. #{i+1}"
    m[i].each do |c|
        puts c
    end
    puts '----'
end
```
* Na classe **Carta**, não se pode alterar diretamente campos como **naipe** e **valor**, são necessários métodos como **getter** e **setter**
    * **Getter**: método com nome do atributo, retorna seu valor
    * **Setter**: método com nome do tipo `<nome-do-atributo>=`
    ```ruby
    class Carta
        def initialize(n, v)
            @naipe = n
            @valor = v
        end

        #getter
        def naipe
            @naipe
        end

        #setter
        def naipe=(n)
            @naipe = n
        end

        def to_s
            return "#{@valor} de #{@naipe}"
        end
    end
    ```
    * **Getter** e **setter** automaticamente: `attr_accessor` seguido com os nomes dos atributos
        * Apenas **getter**: `attr_reader`
        * Apenas **setter**: `attr_writer`
        ```ruby
        class Carta
            attr_accessor :naipe, :valor

            def initialize(n, v)
                @naipe = n
                @valor = v
            end

            def to_s
                return "#{@valor} de #{@naipe}"
            end
        end
        ```