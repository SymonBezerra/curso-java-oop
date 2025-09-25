# Capítulo 6 - Classes Abstratas

Vimos que o polimorfismo pode sobrecarregar métodos já existentes, no capítulo anterior. No entanto, existe ainda uma outra sofisticação em termos de herança e polimorfismo, que permite que definamos métodos sem comportamento prévio, para serem sobrecarregados nas subclasses. Chamamos isso de **classes abstratas**.

Utilizaremos o mesmo exemplo das classes `Veiculo` e `Carro`. Eis a definição da classe `Veiculo` mais uma vez.

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

Vamos agora definir um método `getTipoMotor`. Cada tipo de veículo possui um tipo de motor diferente, então não faz sentido escrevermos um método para sempre sobrescrever o seu comportamento. Podemos definir, portanto, um **método abstrato** (sem comportamento) da seguinte maneira:

```java
public abstract class Veiculo { // para definir métodos abstratos, a classe também deve ser abstrata
    // resto da classe

    public String getTipoMotor(); // sem chaves
}
```

Para termos métodos abstratos, toda a classe deve ser também uma **classe abstrata**, isto é, **uma classe que não pode ser instanciada**. Pensando bem, ninguém faria uma instância de `Veiculo` que não fosse um `Carro`. Então, o que faremos com uma classe abstrata? Só podemos instanciar subclasses dela. Daí vem o nome *classe abstrata de base* (sigla em inglês, ABC).

No entanto, veremos ainda no próximo capítulo um outro tipo de classe abstrata, que consegue ultrapassar o limite da herança única: a **interface**.

## Exercícios