# Capítulo 2 - Encapsulamento

Aprendemos o primeiro dos quatro pilares da POO, a abstração, no capítulo anterior. Provavelmente você já se perguntou algumas vezes porque utilizamos a palavra-chave `public`, que sempre aparece nos *snippets* de código de Java desde o *Hello, World*. Esta palavra-chave diz respeito ao pilar que estudaremos neste capítulo, o encapsulamento.

O presente capítulo está estruturado da seguinte maneira:

1. Introdução
2. Atributos públicos e privados
3. Getters e setters
4. Uma crítica ao encapsulamento

## 2.1 Introdução

Uma das maiores dificuldades de refatorar qualquer código imperativo (o que inclui tanto programação procedural como POO) é o chamado **estado compartilhado** (ou em inglês, *shared state*): diferentes variáveis e objetos (estado/*state*) são compartilhados por diferentes pontos do código, e sem uma manutenção adequada, o nosso código não terá uma manutenção fácil. Isso acontece com mais facilidade em código procedural, onde não há uma regra firme para *encapsular*, ou seja, restringir o acesso ao estado do nosso código.

O pilar de encapsulamento define que alguns atributos e funções podem e devem ser restringidos, para garantir um código mais simples e previsível. Atributos que são irrestritos são chamados de **públicos**, e atributos restritos são chamados de **privados**.

## 2.2 Atributos públicos e privados

Até agora, só definimos atributos públicos através da palavra-chave `public`. Atributos públicos podem ser acessados a qualquer momento e podem também ser redefinidos sem restrições. Vamos utilizar como exemplo nesse capítulo uma classe `Documento`.

```java
public class Documento {
    public String tipo;
    public Long numero;

    // construtor vazio

    public static void main(String[] args) {
        Documento doc = new Documento();
        // escrita livre
        doc.tipo = "Alvará";
        doc.numero = 1001;
        // leitura livre
        System.out.println(doc.tipo);
        System.out.println(doc.numero);
    }
}
```

No entanto, uma vez que um `Documento` é criado, logicamente não deveria ser possível redefinir o seu tipo e o seu número (em outras palavras, isso fere a própria abstração de um documento real). Para isso, deveríamos definir `tipo` e `numero` como atributos privados, isto é, cuja leitura é restrita ao próprio objeto.

```java
public class Documento {
    private String tipo;
    private Long numero;

    // construtor vazio
    public Documento(String t, Long n) {
        tipo = t;
        numero = n;
    }

    public void imprime() {
        // atributos privados só podem ser acessados em métodos
        // definidos dentro do próprio objeto
        System.out.println("Documento n° " + numero + "(" + tipo + ")");
    }

    public static void main(String[] args) {
        Documento doc = new Documento("Certidão de Nascimento", 1000);
        // NÃO COMPILA
        doc.tipo = "Alvará";
        doc.numero = 1001;
        // NÃO COMPILA
        System.out.println(doc.tipo);
        System.out.println(doc.numero);
        // método correto
        doc.imprime();
    }
}
```

Também é possível definir métodos privados:

```java
public class Documento {
    private String tipo;
    private Long numero;

    // construtor vazio
    public Documento(String t, Long n) {
        tipo = t;
        numero = n;
    }

    private void imprime() {
        // atributos privados só podem ser acessados em métodos
        // definidos dentro do próprio objeto
        System.out.println("Documento n° " + numero + "(" + tipo + ")");
    }

    public static void main(String[] args) {
        Documento doc = new Documento("Álvara", 1001);
        // NÃO COMPILA
        doc.imprime();
    }
}
```

O intuito do encapsulamento não é simplesmente restringir o acesso a atributos, mas sim definir regras explícitas para o seu uso. Sendo assim, como podemos fazer para definir um atributo encapsulado, mas que podemos ter acesso?

## 2.3 Getters e setters

É aí que entram dois tipos de métodos especiais: *getters* e *setters*. Eles são métodos públicos que permitem regular o acesso de leitura e escrita a atributos encapsulados. Vejamos no exemplo abaixo:

```java
public class Documento {
    private String tipo;
    private Long numero;

    public Documento(String t, Long n) {
        tipo = t;
        numero = n;
    }

    /* 
        Como atributos privados são acessíveis apenas 
        dentro do escopo da classe, é perfeitamente possível
        realizar a leitura e escrita deles dentro de métodos públicos.
    */
    public String getTipo() {
        return tipo;
    }

    public void setTipo(String tipo) {
        this.tipo = tipo;
    }

    public Long getNumero() {
        return numero;
    }

    public void setNumero(Long numero) {
        /*
            Uma outra utilidade dos setters:
            definir regras para a (re)escrita.
        */
        if (numero > 1000) {
            this.numero = numero;
        }
    }

    public static void main(String[] args) {
        Documento doc = Documento("Alvará", 1000);
        doc.setTipo("Segunda Via de Alvará"); // compila!
        doc.setNumero(1); // compila, porém será ignorado
        System.out.println("Documento n° " + doc.getNumero() + "(" + doc.getTipo() + ")"); // compila!
    }
}
```

Vemos então que existe uma grande utilidade para *getters* e *setters*! Experimente agora criar uma classe `Carta` e uma classe `Carro` com *getters* e *setters*.

Quando devemos utilizar *getters* e *setters*? Utilizando o princípio da abstração, devemos pensar: este atributo deve ser acessível, em leitura e escrita, como estado compartilhado, isto é, em qualquer parte do código? É necessário que este atributo tenha um *setter*, ou apenas um *getter*, sendo um atributo *readonly*? Outra possibilidade é utilizar um *getter* para um "atributo" que não está definido na classe, como por exemplo, `getImpressao` para recuperar a *string* do método `imprime` que definimos antes.

Mesmo com a enorme potencialidade de refatoração e manutenção de código possibilitados pelo pilar de encapsulamento, há algumas críticas muito pertinentes a serem feitas.

## 2.4 Uma crítica ao encapsulamento

Nos últimos anos, o paradigma de POO vem sendo duramente criticado por ter gerado problemas de refatoração tão significativos quanto os que ele tentou resolver ao propor-se como alternativa à programação procedural. Uma das críticas é justamente por conta do excesso de código (*boilerplate*) gerado por vários *getters* e *setters* que, se pararmos para pensar, são praticamente equivalentes a um atributo público.

A linguagem Python, na sua implementação de POO e no seu uso por parte da comunidade, não favorece o uso de atributos encapsulados, não possuindo, por exemplo, palavras-chave para definir atributos públicos e privados. A linguagem Kotlin, que é retrocompatível com o Java, utiliza *getters* e *setters* implícitos que podem ser redefinidos caso haja alguma regra mais complexa. Outras linguagens, como o C#, possuem um recurso chamado ***data class***, que predefine *getters* e *setters* para cada atributo, além de outros métodos especiais que veremos mais à frente. Uma das alternativas no ecossistema Java é usar o pacote Lombok, que possui *annotations* que definem *getters* e *setters* em tempo de compilação.

```java
import lombok.Getter;
import lombok.Setter;

@Getter // define getters na compilação
@Setter // define setters na compilação
public class Documento {
    private String tipo;
    private Long numero;

    public Documento(String t, Long n) {
        tipo = t;
        numero = n;
    }

    public static void main(String[] args) {
        Documento doc = Documento("Alvará", 1000);
        doc.setTipo("Segunda Via de Alvará"); // compila!
        doc.setNumero(1); // compila, porém será ignorado
        System.out.println("Documento n° " + doc.getNumero() + "(" + doc.getTipo() + ")"); // compila!
    }
}
```

## Exercícios