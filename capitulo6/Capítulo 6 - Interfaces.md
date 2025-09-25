# Capítulo 6 - Interfaces

Lembra que falamos que o criador do Java, o cientista James Gosling, disse certa vez que, se não fosse pela pressão comercial, o Java nem teria herança? Então, era por causa das **interfaces** - o conceito que veremos hoje - que ele falou isso. Vimos no último capítulo o conceito de classes abstratas. Vamos lembrar algumas coisas:

1. Uma classe abstrata é uma classe que possui métodos abstratos, isto é, métodos que não possuem comportamento.
2. Um método abstrato é definido apenas escrevendo a assinatura do método.
3. Um método abstrato deve ser obrigatoriamente sobrecarregado nas subclasses.

Agora imaginemos o seguinte caso: e se pudéssemos ter uma classe 100% abstrata? Essa é a definição de uma **interface**: uma classe abstrata, porém composta *apenas* de métodos abstratos.

Vamos colocar um exemplo diferente: implementemos uma estrutura de dados, uma `Lista` e uma `Pilha` (ou como se fala em Python, *dicionário*, ou *hash set* em Java), ambas coleções de *strings*. Não faz sentido definirmos atributos em comum para estas classes, mas podemos definir **métodos em comum**: essa é a função de uma interface.

Vejamos como seria uma interface `Colecao` para ambas estas classes supracitadas.

```java
public interface Colecao {
    public void adicionar(String item);
    public int getTamanho();

    /*
        Outros métodos serão definidos em cada classe
    */
}

public class Lista implements Colecao { // implements ao invés de extends
    private String[] lista;
    private int tamanho = 0;

    @Override
    public void adicionar(String item) {
        lista[tamanho] = item;
        tamanho++;
    }

    @Override
    public int getTamanho() {
        return tamanho;
    } 
    
    // outros métodos
}

public class Pilha implements Colecao {
    private List<String> pilha; // utilizaremos uma List, ao invés de um array simples

    public Pilha() {
        this.pilha = new ArrayList<String>();
    }

    @Override
    public void adicionar(String item) {
        lista.add(item);
    }

    @Override
    public int getTamanho() {
        return lista.size();
    }

    // outros métodos
}
```

> Enquanto no Java uma classe só pode herdar de no máximo uma classe, é possível implementar diversas interfaces.

Vemos que, mesmo tendo um método em comum, os comportamentos são completamente diferentes. Por isso a "herança" múltipla de interfaces é permitida.

## Bônus: Type Generics

Você deve ter observado a declaração `List<String>` e deve ter se perguntado o que significa: entramos no mundo de *type generics*, uma herança dos *templates* da linguagem C++. Podemos definir tipos genéricos para qualquer classe, seja ela abstrata ou não, e também para interfaces.

Podemos definir uma composição de classes genérica no Java através dessa sintaxe. Vejamos uma segunda versão da nossa interface `Colecao`:

```java
public interface Colecao<T> { // por convenção, mantemos a letra T de "type"
    void adicionar(T item);
    int getTamanho();
}

import java.util.ArrayList;
import java.util.List;

public class Pilha<T> implements Colecao<T> {
    private List<T> pilha;

    public Pilha() {
        this.pilha = new ArrayList<>();
    }

    @Override
    public void adicionar(T item) {
        pilha.add(item);
    }

    @Override
    public int getTamanho() {
        return pilha.size();
    }

    // outros métodos

    public static void main(String[] args) {
        Pilha<String> pilha = new Pilha(); // definimos uma pilha de strings
    }
}
```

> Podemos também definir um supertipo específico, como `<T extends Veiculo>`, para termos coleções de objetos do tipo `Veiculo`, definido no capítulo anterior.

Percorremos até aqui todos os conteúdos de orientação a objetos em Java. No próximo capítulo, veremos como tratar exceções, um tipo especial de objeto no Java.