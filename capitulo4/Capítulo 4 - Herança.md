# Capítulo 4 - Herança

Muito bem, já vimos até agora dois dos quatro pilares da POO! Agora, vamos para um dos pilares que tornam esse paradigma tão especial e, ao mesmo tempo, lhe causa mais problemas: o pilar de herança.

O presente capítulo está estruturado da seguinte forma:

1. Introdução
2. Estendendo classes
3. Problemas

## 4.1 Introdução

O pilar de herança é um dos pontos principais da POO que permite a reutilização de código. Vimos que, na programação procedural, se definimos tipos similares, precisaríamos repetir quase todo o código escrito para o primeiro na definição do segundo. Buscar evitar essa repetição, a POO oferece a solução através de *subclasses* (ou classes-filhas) e *superclasses* (ou classes-mãe).

> Utilizaremos a nomenclatura "subclasse" e "superclasse" ao longo deste curso.

## 4.2 Estendendo classes

Vamos definir um tipo "genérico" chamado `Veiculo`. Um veículo pode ligar, desligar, acelerar e frear.

```java
public class Veiculo {
    private String tipo;
    private String marca;
    private String modelo;
    private int anoFabricacao;
    private int velocidade;
    private boolean ligado = false;

    // construtor all-args (com todos os atributos como argumentos), getters e setters...

    public void ligar() {
        ligado = true;
        System.out.println("Veículo ligado!");
    }

    public void desligar() {
        if (!ligado) {
            System.out.println("O veículo já está desligado!");
            return;
        }
        ligado = false;
        System.out.println("Veículo desligado.");
    }

    public void acelerar() {
        if (velocidade == 100) {
            System.out.println("Velocidade máxima atingida!");
            return;
        }
        velocidade++;
        System.out.println("Acelerando veículo...");
    }

    public void frear() {
        if (velocidade == 0) {
            System.out.println("O veículo está parado!");
            return;
        }
        velocidade--;
        System.out.println("Freando veículo...");
    }
}
```

Poderíamos muito bem utilizar o atributo `tipo` para definir diferentes tipos de `Veiculo`. Mas e se quisermos ter uma classe por tipo de veículo? É aí que entra a herança! Vamos definir uma classe `Carro`, que contenha todos os atributos e métodos de `Veículo`:

```java
public class Carro extends Veiculo {
    // contém todos os métodos, atributos e o mesmo construtor
}
```

> No Java, **só é possível herdar de uma única classe**! Veremos como driblar esta limitação no capítulo sobre interfaces.

Porém, e se quisermos definir, no construtor, que o atributo `tipo` terá sempre o valor `Carro`? Vamos redefinir tipo como um `enum`:

```java
public enum TipoVeiculo {
    CARRO,
    MOTO
}

public class Veiculo {
    private TipoVeiculo tipo;
    private String marca;
    private String modelo;
    private int anoFabricacao;
    private int velocidade = 0;
    private boolean ligado = false;

    public Veiculo(TipoVeiculo tipo, String marca, String modelo, int anoFabricacao) {
        this.tipo = tipo;
        this.marca = marca;
        this.modelo = modelo;
        this.anoFabricacao = anoFabricacao;
    }

    // restante da classe
}
```

Agora vamos definir um construtor explícito para `Carro`, que estende a classe `Veiculo`:

```java
public class Carro extends Veiculo {
    private int aroPneu; // podemos definir novos atributos
    public Carro(String marca, String modelo, int anoFabricacao, int aroPneu) {
        /*
            Assim como o `this` referencia a classe,
            o ponteiro `super` referencia a instância
            subjacente da superclasse.
        */
        super(TipoVeiculo.CARRO, marca, modelo, anoFabricacao);
        this.aroPneu = aroPneu;
    }

    // getters, setters e outros métodos
}
```

Vamos nos demorar um pouco sobre o `super`: toda classe `Carro` é também uma classe `Veiculo`, de modo que seria possível dizer:

```java
    Veiculo carro = new Carro("Fiat", "Uno", 1996);
```

No entanto, há um detalhe sobre a tipagem: digamos que definimos um método `abaixarJanelas` apenas para `Carro`.

```java
Veiculo carro = new Carro("Fiat", "Uno", 1996);
Carro carro2 = new Carro("Fiat", "Uno", 2009);

carro.abaixarJanelas(); // não compila, pois Veiculo não possui a definição do método
carro2.abaixarJanelas(); // correto
```

Veremos mais sobre o compartilhamento e até como sobrescrever métodos e atributos de uma superclasse no próximo capítulo. Por enquanto, tente criar uma superclasse `Documento` com alguns atributos e pense em subclasses como `Alvara`, `CertidaoNascimento`, `CertidaoCasamento` como elas seriam.

## 4.3 Problemas

Herança é um dos principais pontos fortes da POO, mas ao mesmo tempo, é um dos seus pontos mais fracos. O próprio criador do Java, o cientista James Gosling, disse certa vez que, se não fosse pela pressão comercial, teria lançado o Java sem herança, já que a linguagem possui alguns truques para evitar os problemas que este pilar traz consigo.

Digamos que o método `usarCintoDeSeguranca` estivesse definido em `Veiculo`. Se criássemos uma classe `Moto extends Veiculo`, o método de usar cinto de segurança, mesmo que não faça sentido algum para uma moto, ainda estaria presente lá. Ou seja, a herança pode fazer com que subclasses tenham comportamentos inúteis, ou que façam sentido apenas para a superclasse.

É por isso que existe o próximo pilar da POO, o polimorfismo, que nos permite alterar comportamentos e atributos da superclasse dentro de uma subclasse para melhor adequá-los às mesmas. Também veremos maneiras mais avançadas de implementar polimorfismo nos capítulos seguintes.

## Bônus: o modificador `protected`

Há algo que não abordamos ainda aqui: o que acontece quando misturamos encapsulamento com herança? Atributos e métodos privados não são visíveis, ou seja, não podem ser acessados, por subclasses. Ou seja, não seria possível acessar nenhum dos atributos que definimos na classe `Veiculo` dentro da classe `Carro`, apenas através dos métodos públicos que já foram definidos na superclasse.

É aí que entra o modificador `protected`, um terceiro encapsulador: quando um atributo ou método é `protected`, ele não pode ser acessado publicamente, mas é visível para todas as superclasses. No nosso caso, faria sentido definir a classe `Veiculo` da seguinte maneira:

```java
public class Veiculo {
    protected TipoVeiculo tipo;
    protected String marca;
    protected String modelo;
    protected int anoFabricacao;
    protected int velocidade = 0;
    protected boolean ligado = false;

    // restante da classe
}

public class Carro extends Veiculo {
    public void consulta() {
        // sem o protected, esta linha não compila
        System.out.println("Modelo: " + marca + " " + modelo + " " + ano);
    }
}
```

## Exercícios