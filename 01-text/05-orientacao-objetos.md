# 05 - Orientação a Objetos
* Construção de abstração, não voltado a definir a sequência de operações (programação imperativa) mas à modelagem dos dados e informações tratadas pelo programa, a fim de facilitar a programação
* **Vantagens**
    * Reutilização de código
    * Extensibilidade
    * Independência de implementação

### Características Objeto
* Tudo é objeto, qualquer elemento do programa é um objeto, sendo até mesmo o programa em si um objeto
* **Programa**: coleção de objetos que interagem
* Objetos podem ser compostos por outros
* Todo objeto tem tipo, ou seja, instância de uma classe
* Classes podem ter subclasses (restrições aos conjuntos que as classes representam)
* Objetos de mesma classe reagem da mesma maneira

### Descrição de Objeto específico
* **Estado**: conjunto de variáveis
* **Comportamento**: métodos
* **Identidade**: instância do objeto (endereço de memória associado)

### 5.1 - Encapsulamento
* Toda classe preferencialmente esconderá a implementação, definindo uma interface de interação com os objetos dessa classe. Sendo assim, um objeto de outra classe que venha a interagir com essa classe inicial não precisa conhecer detalhes de implementação, apenas como se dá a interação de um objeto da classe em questão

### 5.2 - Herança
* Para atingir um caso mais específico de uma classe já existente, não se faz necessário reconstruir a implementação, apenas aplicando novas restrições ao novo caso
* Em qualquer lugar que se use um objeto da classe original, pode-se utilizar a nova classe derivada, sem necessidade de reprogramar
* A classe derivada pode usar a mesma interface da original, mas faz-se possível **sobrecarregar(override)** métodos, mudando sua implementação
* **Função Virtual**: função sem implementação, apenas definida na interface, **precisando** ser definida em alguma subclasse
* **Formas de Herança**
    * **Especialização**: troca de métodos por outros mais específicos
    * **Extensão**: adição de novos campos e métodos

### 5.3 - Polimorfismo
* Funções podem precisar atuar de maneiras diferentes para classes com alguma similaridade, sendo a chamada escrita do mesmo jeito
    * Faz-se necessário busca em tempo de execução (**late binding**), pois pode ser possível definir a função a ser executada apenas em tempo de execução
* Outro exemplo são para funções que podem receber tipos diferentes de objetos como argumentos, apresentando implementações diferntes de acordo como tipo de argumento