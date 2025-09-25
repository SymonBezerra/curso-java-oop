# Capítulo 1 - Orientação a Objetos

Muito bem, você concluiu os seus primeiros passos na linguagem Java. Você aprendeu como a linguagem Java é executada, os seus tipos de dados básicos, como declarar variáveis, estruturas condicionais, *loops*, como manipular *strings* e como escrever funções. Agora está na hora de aprender um pouco do paradigma que norteia toda a filosofia da linguagem Java: a orientação a objetos.

1. Introdução
2. Os Quatro Pilares
3. Abstração
4. Métodos e atributos estáticos

## 1.1 Introdução

Vimos no capítulo anterior como organizarmos o nosso código em funções. Nos primórdios da programação, sequer elas existiam. Aos poucos surgiram as **subrotinas**, em linguagens como o BASIC (que foi muito popular nos computadores domésticos de 8 bits dos anos 70 e 80). No entanto, havia um pequeno problema: o código ainda contava com instruções muito similares às instruções de linguagens de máquina (*assembly*).

Uma dessas instruções era o ***goto***, que realizava saltos no código (algo que é extremamente comum em *assembly*, mas que prejudica bastante a legibilidade de um código de alto nível). Assim, o código começou a se organizar inteiramente em funções e procedimentos (para nós, procedimento seria apenas uma função que não retorna nada, ou do tipo `void`). Surgiu, assim, a programação procedural.

O mundo procedural foi extremamente importante e ainda é o paradigma principal de linguagens como o C, esta que por sua vez constrói praticamente tudo que está a nossa volta em termos computacionais, de uma maneira ou outra. No entanto, a programação procedural, estruturada apenas em funções, tem algumas limitações.

- Repetição de código: reutilizar código procedural é algo difícil. Por exemplo, se criarmos uma série de procedimentos na nossa biblioteca para livros, precisaremos criar outros procedimentos para revistas, outros para artigos acadêmicos, e assim por diante.

- Falta de proteção de dados: como não há um encapsulamento natural, manter código procedural é difícil graças ao *shared state* (estados compartilhados). Em outras palavras, qualquer um pode acessar qualquer ponto do código a qualquer momento, e não é possível, em termos de programação, implementar uma regra que diga o contrário.

- Manutenção: tipos de dados compostos e funções ficam separados, tornando assim difícil manter um e outro.

O paradigma de orientação a objetos, mesmo que não seja perfeito, oferece algumas soluções para isso. A programação orientada a objetos (doravante, POO) é um paradigma de programação que organiza o código em objetos - unidades que combinam dados e comportamentos relacionados em uma única estrutura coesa. Em essência, a POO transforma programas de uma coleção de funções processando dados soltos para um sistema de objetos colaborativos, onde cada um é responsável por seus próprios dados e comportamentos, tornando o código mais organizado, reutilizável e escalável.

## 1.2 Os Quatro Pilares

A POO é definida em quatro pilares:

1. Abstração: é possível definir unidades de código abstratas, isto é, não é necessário conhecer a implementação subjacente de um objeto para utilizá-lo. Isto torna os objetos mais utilizáveis e fáceis de realizar manutenção.
2. Encapsulamento: é possível definir variáveis e funções completa ou parcialmente isoladas do mundo externo, isto é, inacessíveis em outros lugares do código.
3. Herança: é possível definir tipos compostos que são subtipos de outros objetos, reaproveitando boa parte do código já implementado.
4. Polimorfismo: ao mesmo tempo que é possível reaproveitar código, é possível modificar o código reaproveitado.

Neste capítulo, falaremos mais sobre o pilar da Abstração, e nos capítulos seguintes, detalharemos os conceitos sobre os demais pilares.

## 1.3 Abstração

Antes, precisamos introduzir o conceito de **objeto**. O que é um objeto? Vimos no capítulo anterior que o Java possui tipos primitivos - sendo que `String` não é um deles. Um objeto é um tipo composto que encapsula variáveis e funções em uma mesma unidade computacional. Todo o nosso mundo, de agora em diante, será guiado por objetos. Pensemos um exemplo simples: um objeto `Carro`. Um carro possui uma marca, modelo e ano de fabricação - estes seriam seus atributos. Alguns comportamentos do objeto `Carro`, isto é, uma função do objeto `Carro` seria ligar, acelerar, freiar e desligar.

> No mundo da POO, funcionalidades são geralmente chamadas de **comportamentos**, isto é, coisas que os objetos podem fazer. Também as funções e procedimentos, quando dentro da definição de um objeto, são chamadas de **métodos**. De agora em diante, utilizaremos essas definições.

Vejamos como seria a definição de um objeto `Carro` em Java. Não se preocupe, explicaremos passo a passo cada coisa.

```java
public class Carro {
    public String marca;
    public String modelo;
    public int anoFabricacao;

    public Carro(String marca, String modelo, int anoFabricacao) {
        this.marca = marca;
        this.modelo = modelo;
        this.anoFabricacao = anoFabricacao;
    }
}
```

Muita coisa nova né? Calma, veremos passo a passo cada coisa. Começamos lembrando do padrão `PascalCase` para nome de classes, como vimos no capítulo anterior. Primeiro, iremos definir, fora de qualquer método, os **atributos** desta classe: `marca`, do tipo `String`; `modelo`, também do tipo `String`, e `anoFabricacao`, um número inteiro. Estas serão as variáveis que compõem o objeto. Por enquanto, convencionemos que devemos sempre utilizar a palavra-chave `public` antes do tipo de dado (entenderemos isso quando falarmos de encapsulamento).

Depois, definiremos um método especial, chamado com o mesmo nome da classe. Observe que ele não tem um tipo explícito, pois ele retorna um objeto do tipo `Carro`. Este método é chamado de **construtor**. Imaginemos que estamos *instanciando*, ou seja, criando um objeto `Carro`. Seria algo mais ou menos assim:

```java
public class Carro {
    public String marca;
    public String modelo;
    public int anoFabricacao;

    public Carro(String marca, String modelo, int anoFabricacao) {
        this.marca = marca;
        this.modelo = modelo;
        this.anoFabricacao = anoFabricacao;
    }

    public static void main(String[] args) {
        Carro carro = new Carro("Fiat", "Uno", 1996); // só falta o atributo booleano `escadaNoTeto`!
    }
}
```

Esta linha, com a palavra chave `new`, chama diretamente o método construtor. Ou seja, assim como o `main` é o ponto de entrada do programa, o construtor é o ponto de entrada do objeto. Por padrão, toda classe possui um construtor vazio. Ao definirmos um construtor, este construtor não pode ser mais utilizado, a menos que o definamos explicitamente. Como construtores são funções, tudo o que vimos sobre valores padrões se aplica aqui.

```java
public class Carro {
    public String marca;
    public String modelo;
    public int anoFabricacao = 1900; // valor predefinido, por padrão é null

    public Carro(String marca, String modelo, int anoFabricacao) {
        this.marca = marca;
        this.modelo = modelo;
        this.anoFabricacao = anoFabricacao;
    }

    // é possível ter mais de um construtor para uma mesma classe
    public Carro() {
        // todos os valores são inicializados como `null`
    }
}
```

Outra coisa que precisamos entender é o ponteiro `this`. O que significa esta palavra? Basicamente, ele é uma variável que aponta para o objeto que chamou o método. Vejamos nesse exemplo:

```java
public class Carro {

    public void printAno() {
        System.out.println("Ano de fabricação: " + this.anoFabricacao);
    }

    public static void main(String[] args) {
        Carro carro1 = new Carro("Fiat", "Uno", 1996);
        Carro carro2 = new Carro("Fiat", "Uno", 2009);
        carro1.printAno(); // 1996
        carro2.printAno(); // 2009
    }
}
```

Ou seja, o `this` aponta para a **instância** do objeto que chamou o método. Já está na hora de entendermos o que são instâncias e classes. **Classe** seria a definição do tipo `Carro`, enquanto uma **instância** é uma variável `Carro` com atributos definidos.

```java
public class Carro { // esta é a definição de `Carro`, a CLASSE
    public String marca;
    public String modelo;
    public int anoFabricacao;

    // construtor vazio

    public static void main(String[] args) {
        Carro carro = new Carro(); // INSTÂNCIA do tipo Carro
    }
}
```

> Ainda sobre o `this`: no Java, `this` é, na maioria dos casos, **opcional**. Por exemplo, no exemplo do método `printAno`, não seria necessário usar `this.anoFabricacao`. Ele é apenas obrigatório quando há ambiguidade, ou seja, quando chamamos um método com argumentos de nomes iguais aos atributos, como no caso do construtor que definimos, onde há uma variável do método de mesmo nome para cada atributo. Para evitar o uso de `this`, poderíamos usar outros nomes para os argumentos do construtor.

Tudo o que vimos até agora define também o conceito do pilar de Abstração da POO: abstrair significa criar unidades reutilizáveis de código cuja definição não precisa ser conhecida a fundo para ser utilizada (o que muitas vezes é necessário no mundo procedural). Como primeiro exercício, experimente criar agora um tipo `Carta` (carta de baralho), tente definir seus atributos, seu construtor e um método `mostrarCarta`.

## 1.4 Métodos e atributos estáticos

Agora que falamos sobre métodos e atributos, isto é, funções e variáveis que pertencem aos objetos, podemos finalmente responder a uma pergunta: o que significa o modificador `static`, do `public static void main`? Bom, `void main` é a definição da função. A palavra `public` será explicada no capítulo seguinte, sobre encapsulamento.

Quando definimos um método ou atributo estático, ele não pertence ao objeto, mas sim à classe; pertence ao tipo, e não às instâncias. Vejamos um exemplo mais claro com uma classe `Carta` (carta de baralho):

```java
public class Carta {
    public static String marca = "Copag"; // este curso não é patrocinado, mas bem que poderia

    public String naipe;
    public String valor;

    public Carta(String naipe, String valor) {
        this.naipe = naipe;
        this.valor = valor;
    }

    public static void imprimeMarca() {
        System.out.println("Cartas da Copag ©");
    }

    public static void main(String[] args) {
        System.out.println(Carta.marca); // "Copag";
        System.out.println(Carta.imprimeMarca()); // "Cartas da Copag ©"
        Carta c = new Carta("Espadas", "Ás");
        System.out.println(c.marca); // não compila, pois o método é estático
        System.out.println(c.imprimeMarca()); // não compila, pois o método é estático
    }
}
```

O atributo `marca` pertence ao tipo `Carta` em si, e não pode ser invocado por nenhuma instância de `Carta`. Podemos utilizar atributos e métodos estáticos quando precisamos de funções e variáveis que não pertençam a nenhuma instância em si, mas sim ao tipo como um todo. Porém, precisamos ter moderação ao usar métodos estáticos, ou recaíremos em uma programação puramente procedural.

## Bônus: o tipo *enum*

Existe um objeto especial no Java e em outras linguagens, o enumerador ou `enum`. Ele é um objeto de um ou mais atributos, cujo construtor é privado, ou seja, possui instâncias já predefinidas.

Vejamos um exemplo:

```java
public enum Naipe {
    /*
        Todo enum possui um valor ordinal,
        que começa a partir de zero e é atribuído
        a partir da ordem que as enumerações são destacadas.
    */
    OUROS, // 0
    ESPADAS, // 1
    COPAS, // 2
    PAUS; // 3
}
```

É possível definir atributos para um `enum`, porém todos eles são `final` (constantes):

```java
public enum Naipe {
    OUROS("Mole"),
    ESPADAS("Espadilha"),
    COPAS("Copeta"),
    PAUS("Zap");

    public final String apelido;

    private Naipe(String apelido) {
        this.apelido = apelido;
    }
}
```

Alguns métodos para o nosso `enum`:

```java
Naipe n = Naipe.OUROS;
System.out.println(n.apelido); // Mole
System.out.println(n.ordinal()); // 0
```

## Exercícios