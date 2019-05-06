# 09 - Herança Múltipla
* Objeto com características de dois tipos diferentes (extende mais de uma classe base)
    * Problemas:
        * Herdar implementações diferentes dos mesmos métodos ou ser derivada da mesma vase
        * Campo de ancestral comum pode ser modificado indiretamente por outros métodos

### Exemplo - Hierarquia de Alimentos
* Alimento
    * Sólido
        * Carne
        * Ovo
        * Fruta
        * Sais
    * Líquido
        * Aquoso
            * Água
            * Leite
            * Suco
        * Óleo
<br><br>
* Sem uso de herança múltipla: **mixins**
    * Declaram métodos que podem ser utilizados em outras classes
    * **Ruby**: mixins definidos em **modules**
        * Classe C que inclua um 'module M' recebe os métodos definidos em M
```ruby
#!/usr/bin/env ruby
# coding: utf-8

module Fritavel
    @frito = false
    def fritar
        print self.class.name
        if @frito
            puts " >>> Torrou"
        else
            puts " > [Barulho de fritura.mp3]"
            @frito = true
        end
    end
end

class Alimento
end

class Solido < Alimento
end

class Carne < Solido
    include Fritavel
end

class Ovo < Solido
    include Fritavel
end

class Fruta < Solido
end

class Sais < Solido
end

class Liquido
end

class Aquoso < Liquido
end

class Agua < Aquoso
end

class Leite < Aquoso
end

class Suco < Aquoso
end

class Oleo < Liquido
    include Fritavel
end

perrier = Agua.new

bife = Carne.new
bife.fritar
codorna = Ovo.new
codorna.fritar

bife.fritar
```

### Comparador Total - `<=>`
* Retorna -1, 0 ou 1 se o valor da esquerda é menor, igual ou maior ao valor da direita
* Há também o módulo `Comparable`
```ruby
class SizeMatters
    include Comparable

    def <=>(other)
        str.size <=> other.str.size
    end
    
    def initialize(str)
        @str = str
    end

    def inspect
        @str
    end
end

s1 = SizeMatters.new("Z")
s2 = SizeMatters.new("YY")
s3 = SizeMatters.new("XXX")
s4 = SizeMatters.new("WWWW")
s5 = SizeMatters.new("VVVVV")

s1 < s2  # true
s4.between?(s1, s3)  # false
s4.between?(s3, s5)  # true
[s3, s2, s5, s4, s1].sort  # [Z, YY, XXX, WWWW, VVVVV]