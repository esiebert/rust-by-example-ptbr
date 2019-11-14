# Expressoes

Um programa Rust é (sobretudo) feito por vários comandos:

```
fn main() {
    // comando
    // comando
    // comando
}
```

Existem poucos comandos em Rust. Os dois mais comuns sendo declaracao um vínculo de variável, 
e usando ';' com uma expressao:

```
fn main() {
    // Declaracao de variável
    let x = 5;

    // expressao;
    x;
    x + 1;
    15;
}
```

Blocos sao expressoes também e podem ser usadas como valores em atribuicoes.
A última expressao em um bloco será atribuída a um lugar, como uma variável local.
Porém, se a última expressao do bloco terminar com ';', o valor retornado será `()`.

```rust,editable
fn main() {
    let x = 5u32;

    let y = {
        let x_quadrado = x * x;
        let x_cubico = x_quadrado * x;

        // Essa expressao será atribuída à `y`
        x_cubico + x_quadrado + x
    };

    let z = {
        // O ';' reprime essa expressao e `()` é atribuído à `z`
        2 * x;
    };

    println!("x é {:?}", x);
    println!("y é {:?}", y);
    println!("z é {:?}", z);
}
```
