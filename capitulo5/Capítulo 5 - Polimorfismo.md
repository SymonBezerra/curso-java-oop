# Capítulo 5 - Polimorfismo

Vimos no capítulo anterior que, ao mesmo tempo que possui muitos prós, o pilar de herança traz consigo muitos contras que precisam ser levados em conta. Uma das maneiras de contornar estes problemas é justamente através do quarto e último pilar: o polimorfismo.

O presente capítulo está estruturado da seguinte forma:

1. Introdução
2. Sobrecarga de métodos
3. Alternativas avançadas

## 5.1 Introdução

Vimos que a herança apresenta um problema fundamental: trazer consigo comportamentos em excesso, e que ela deve ser usada com sabedoria. Uma das soluções que o Java apresenta é não permitir herança de múltiplas classes (o que é permitido em classes como C++ e Python). No entanto, a própria POO oferece também uma "solução", ou melhor, um incremento à herança: o pilar do polimorfismo (do grego, muitas formas).

## 5.2 Sobrecarga de métodos

Voltemos ao exemplo da classe `Carro` e sua superclasse `Veículo`. Vemos que os prints estão dizendo: "Veículo realiza" tal ação. E se quiséssemos que, por padrão, o `Carro` dissesse "Carro" ao invés de "Veículo". Uma das formas de se alcançar este comportamento é através da **sobrecarga de métodos**.

> Basicamente, a sobrecarga de métodos sobrescreve um método de uma superclasse com um novo comportamento.

Vejamos de novo a implementação da classe `Veiculo`:

```java
public class Veiculo {
    protected String tipo;
    protected String marca;
    protected String modelo;
    protected int anoFabricacao;
    protected int velocidade;
    protected boolean ligado = false;

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

Se quisermos sobrescrever o método `ligar`, podemos fazê-lo declarando o mesmo método, com o mesmo tipo de retorno, utilizando a *annotation* `@Override`:

```java
public class Carro extends Veiculo {
    @Override // anotação de sobrecarga
    public void ligar() {
        ligado = true;
        System.out.println("Carro ligado!");
    }
}
```

Agora digamos que o método original não tivesse nenhum `println`, e só atribuísse o valor `true` à variável `ligado`, da seguinte maneira:

```java
public class Veiculo {
    // restante da classe

    public void ligar() {
        ligado = true;
    }

    // restante da classe
}
```

Podemos reaproveitar esse comportamento através do ponteiro `super`:

```java
public class Carro {
    @Override
    public void ligar() {
        super.ligar(); // assim, utilizamos ambos os comportamentos
        System.out.println("Carro ligado");
    }
}
```

Algumas anotações sobre polimorfismo em Java:

1. Não é possível mudar a visibilidade do método (por exemplo, transformar método público em privado).
2. Mesmo que utilizemos uma variável `Veiculo v = new Carro(...)` e façamos a chamada `v.ligar()`, o método chamado será o método sobrecarregado na subclasse.
3. É possível sobrescrever valores padrão de atributos, mas não o seu tipo ou visibilidade.

```java
public class Veiculo {
    public TipoVeiculo tipo;
}

public class Carro extends Veiculo {
    public TipoVeiculo tipo = TipoVeiculo.CARRO; // deve ter mesmo nome, tipo e visibilidade
}
```

## 5.3 Alternativas avançadas

Apenas a sobrecarga de métodos não funciona. Em teoria, poderíamos passar um método vazio, mas isso não seria suficiente: alguém poderia simplesmente esquecer de sobrecarregá-lo. Talvez precisemos de algo mais... *abstrato* ainda. É aí que entram as *abstract base class* (classes abstratas de base), ou ABCs. Veremos mais sobre elas no próximo capítulo.

## Exercícios