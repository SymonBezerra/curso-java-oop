# Capítulo 1 - Introdução ao Java

Seja bem vindo ao nosso curso da linguagem de programação Java. Nesse primeiro capítulo, você aprenderá sobre as estruturas básicas da linguagem, desde o seu primeiro programa até criar funções.

Nosso capítulo será estruturado da seguinte maneira:

1. Hello World!
2. Variáveis e Tipos de Dados
3. Estruturas Condicionais
4. Estruturas de Repetição
5. Manipulação de Strings
6. Estruturas de Dados
7. Funções

## 1.1 Hello World!

Como em qualquer linguagem, o primeiro passo é escrever um programa que retorne algum texto à saída padrão (`stdout`) da máquina. Vejamos, portanto, um primeiro exemplo de código na linguagem Java.

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Talvez você tenha se assustado um pouco com a complexidade de um simples `Hello World`...mas não se preocupe, entenderemos tudo ao longo desse curso. Por hora, você deve se atentar aos seguintes detalhes:

- A linha principal chama a função `println`, do módulo `System.out` (saída de sistema). Essa é a função de imprimir texto na saída padrão (`stdout`) da linguagem Java. Algumas IDEs possuem um atalho para este comando, como no caso do VSCode, `sout`.

- Java é uma linguagem orientada a objetos, onde *absolutamente tudo* são classes. Entenderemos mais sobre isso depois, porém tudo o que você precisa saber por hora é que você deve criar uma classe com o mesmo nome do seu arquivo. Falando em nomes, o Java utiliza preferencialmente o padrão `PascalCase` (palavras juntas, sempre com inicial maiúscula) para nomes de classes.

- Não se preocupe com `public`, `static`, `void`, `main`, `String[]`, `args`. Tudo o que você precisa agora saber é que um programa Java é inicializado a partir do arquivo que contém esta função principal (`main`).

- A depender da sua IDE, essa função já vem escrita ao criar um projeto Java. Caso contrário, basta utilizar o atalho `main`.

> Curiosidade: o programa "Hello, World!" foi criado pelo cientista Brian Kernighan, no livro tutorial da linguagem de programação B, uma linguagem interpretada que posteriormente deu origem ao C, cuja sintaxe inspirou fortemente a linguagem Java.

## 1.2 Variáveis e Tipos de Dados

### Java - Linguagem compilada ou interpretada? Os dois!

Aprendido o primeiro programa da linguagem Java, passemos agora ao próximo passo: aprender sobre variáveis e tipos de dados. Primeiro, é necessário entender duas coisas fundamentais sobre a linguagem Java, que tornam ela bastante especial. Primeiro, Java é uma linguagem de **tipagem estática**, o que significa que o tipo de uma variável é checado no ato de compilação.

O segundo ponto - preste bastante atenção agora - é que o Java é uma linguagem compilada, ou seja, o seu código é transformado em ***bytecode*** para ser executado em uma máquina virtual. Linguagens compiladas geralmente transformam seus códigos em executáveis (no caso do ecossistema Windows, é isso que significa a extensão `.exe`), que nada mais são do que arquivos binários. Ou seja, todas as instruções que colocamos, como o comando de imprimir "*Hello, World*", são transformadas em zeros e uns. Para abstrair essas instruções, existem linguagens de montagem, como o *Assembly*, que nada mais é do que um equivalente de um para um para instruções binárias. Porém, há uma limitação para as linguagens compiladas: arquivos executáveis são feitos apenas para uma arquitetura de sistema operacional, já que cada SO organiza-se de maneira diferente à nível de arquitetura computacional. Isto é, um arquivo `.exe` do Windows não pode rodar no Linux, e um arquivo `.out` do Linux não pode rodar em um Mac.

Linguagens interpretadas contornam isso utilizando um interpretador, ou seja, um programa já compilado, para executar suas instruções em diversas arquiteturas diferentes. É o caso da linguagem Python (que é a primeira linguagem de programação de muitos cursos universitários, seguida pelo Java), cujo interpretador é escrito em C. Ou seja, basta escrever o mesmo interpretador para sistemas diferentes. O problema é que linguagens interpretadas adicionam um passo a mais na tradução do código para instruções binárias: ao invés de rodar instruções binárias pré-compiladas, a compilação é praticamente feita no tempo de execução (*runtime*).

O Java, por sua vez, segue uma via média: ele possui sua própria máquina virtual, a *Java Virtual Machine* (JVM). A JVM possui sua própria linguagem de *bytecode*, ou seja, suas próprias instruções binárias. Nesse caso, o nosso *Hello, World* será compilado não para um binário que executa diretamente no sistema operacional (ex.: Windows), mas sim para o *bytecode* da JVM. Isto é, ao clicarmos para executar o nosso programa, ele será primeiro compilado para *bytecode* JVM, e este *bytecode* será interpretado pela própria JVM.

Para executar os programas, será instalado o *Java Runtime Environment* (JRE), que nada mais é do que a JVM com algumas bibliotecas adicionais. E ainda, para desenvolvimento, será utilizado o *Java Development Kit* (JDK), que possui dentro de si a JRE e a JVM. Conseguiu entender cada sigla? O mais importante é entendermos que cada variável será analisada em tempo de compilação do código Java para *bytecode* JVM e, caso haja algum erro de tipagem, o nosso código simplesmente não vai compilar. Não se preocupe, a sua IDE provavelmente irá lhe avisar de um erro antes de você tentar executar ou compilar o seu código.

> Para entender mais sobre *bytecode* e sistemas operacionais, leia o livro "Sistemas Operacionais" de Andrew S. Tanembaum.

### Variáveis e tipos de dados

Vamos começar entendendo alguns tipos de dados. Primeiro, os tipos numéricos:

```java
public class TiposDeDados
    // Olha só, um comentário! Esta linha não define código, e é ignorada pelo compilador.
    public static void main (String[] args) {
        int num1 = 1; // número inteiro, 32 bits
        long num2 = 1000000; // número inteiro, 64 bits
        float num3 = 0.5; // decimal, 32 bits
        double num4 = 0.000001; // decimal, 64 bits ← MAIS UTILIZADO!
        boolean logico = true; // ou `false`
    }
```

Estes são alguns dos tipos básicos de dados. Existem também o `byte` (número de 8 bits, sem sinal, ou seja, não possui número negativo), o `short` (16 bits inteiro, ou seja, com sinal), e também o tipo `char`, que pode representar caracteres Unicode (ou seja, corresponde a um número inteiro de 16 bits).

O tipo `char` pode ser declarado também utilizando caracteres:

```java
char caractere = 'a'; // aspas simples!
```

Há operadores aritméticos na linguagem Java:

```java
char num1 = 1;
char num2 = 2;
int soma = num1 + num2; // em geral, operações com `char`, `short` e `byte`, é feita uma conversão automática para `int`
int multiplicacao = num1 * num2;
int subtracao = num1 - num2;
double divisao = num1 / num2; // retorna um número flutuante
int resto = num1 % num2;
int divisaoInteira = num1 / num2; // como é declarado como inteiro, é ignorada a parte decimal
```

A ordem de precedência dos operadores segue a lógica da aritmética padrão: multiplicação e divisão, depois soma e subtração. É possível também fazer:

```java
int somaPrecedencia = (1 + 1) * 2;
```

Alguns outros pontos que devemos notar até aqui:

- Java segue uma sintaxe inspirada na linguagem C, ou seja, blocos de código são delimitados por chaves (`{` e `}`), e uma linha nova é delimitada por ponto e vírgula (`;`). Isso significa que é possível escrever um programa inteiro em uma única linha de código, mas em nome da legibilidade, não faça isso! No entanto, é possível economizar algumas linhas utilizando instruções na mesma linha separadas por ponto e vírgula. É importante ter bom senso.

- As variáveis do Java seguem o padrão `camelCase` (palavras juntas, com inicial da primeira palavra minúscula e demais palavras com inicial maiúscula).

Até aqui, não falamos de um tipo de dados, o tipo `String` (cadeia de caracteres). Uma informação importante, que só vamos entender mais à frente, é que *strings* não são um tipo primitivo no Java, e sim um tipo composto, ou objeto. Isso confere ao tipo `String` algumas especificidades. Teremos uma seção sobre como manipular *strings*.

```java
String texto = "Hello, World!" // aspas duplas!
```

O que diferencia um tipo de dado de outro é o seu tamanho em *bytes*, ou seja, a quantidade de bits utilizada para armazenar esta variável na memória RAM. Em sistemas com limitação de memória, como microcontroladores, esta é uma informação bem relevante. Mas como desenvolvemos em máquinas com *gigabytes* de memória (ordem de $2^{30}$), não precisamos nos preocupar tanto com isso. Saiba apenas que, em termos gerais:

- Números inteiros, `int`
- Números decimais, `double`
- Valor lógico, `boolean`
- Textos, `String`

### Bônus: o valor *null*

## 1.3 Estruturas Condicionais

Conhecendo agora nossos primeiros tipos de dados, principalmente o tipo booleano, podemos começar a entender estruturas condicionais, a saber, as palavras-chave `if` e `else` ("se" e "caso contrário").

O que são estruturas condicionais? São instruções dentro de um bloco de código condicional, ou seja, estas instruções só serão executadas se uma determinada condição for satisfeita. Vejamos um exemplo:

```java
public class EstruturaCondicional {
    public static void main(String[] args) {
        boolean condicao = true;
        if (condicao == true) {
            System.out.println("Condição satisfeita, olá");
        }
    }
}
```

Vemos aqui a estrutura básica de um condicional `if`: palavra-chave, e uma condição delimitada entre parênteses. O operador `==` é um operador de comparação, ao invés do operador `=`, que é de atribuição. Ou seja, enquanto o `=` atribui um valor à uma variável, o operador `==` compara dois valores. Nesse caso, `condicao == true` é redundante, já que o operador `==` sempre retorna um valor booleano. Ou seja, basta escrevermos:

```java
if (condicao) {
    // código condicionado
}
```

O que aconteceria se `condicao` fosse `false`? O `println` nunca executaria! Mas e se quiséssemos ter um outro `println` para o caso da primeira condição não ser satisfeita? É aí que entra o `else`:

```java
if (condicao) { // se `condicao` for verdadeiro
    System.out.println("Condição satisfeita!");
} else { // Observe que ele não precisa de uma condição entre parênteses
    System.out.println("Condição NÃO satisfeita!");
}
```

Mas e se quiséssemos uma terceira, ou quarta, ou até uma quinta condição!? Podemos unir `if` e `else`:

```java
boolean condicao1 = true;
boolean condicao2 = false;

if (condicao1) {
    // código
} else if (condicao2) {
    // código
} else {
    // código
}
```

Sendo assim, podemos encadear quantos `else if` quisermos! Porém, um detalhe importante: quando há uma estrutura de `if`-`else if`-`else`, **apenas a primeira condição satisfeita é executada**. Ou seja, se a primeira condição for verdadeira, as outras são simplesmente ignoradas. Se quisermos que todas as condições sejam avaliadas, usaremos apenas estruturas `if`, pois `if`'s independentes não são encadeados. Tente experimentar os seguintes códigos, alterando os valores de `condicao1` e `condicao2`:

### Código 1

```java
boolean condicao1 = true;
boolean condicao2 = false;

if (condicao1) {
    System.out.println("Condição 1");
} else if (condicao2) {
    System.out.println("Condição 2");
} else {
    System.out.println("Condição 3");
}
```

### Código 2

```java
boolean condicao1 = true;
boolean condicao2 = false;

if (condicao1) {
    System.out.println("Condição 1");
}
if (condicao2) {
    System.out.println("Condição 2");
}
```

As estruturas condicionais são importantes para criarmos fluxos condicionais nos nossos códigos, por exemplo, se um aluno é ou não aprovado.