# Debug

Todos os tipos que desejam utilizar os `tratis` de formatacao `std::fmt`
exigem uma implementacao para que sejam printaveis. Implementacoes automáticas
sao apenas disponíveis para tipos da biblioteca padrao `std`. Todos outros
*precisam* ser implementados manualmente de alguma forma.

O `trait` `fmt::Debug` facilita essa tarefa. *Todos* tipos podem usar
`derive` para derivar (criar automaticamente) a implementacao de `fmt::Debug`.
Isso é oposto ao `fmt::Display` que deve ser implementado manualmente.

```rust
// Essa estrutura nao pode ser printada com `fmt::Display` ou `fmt::Debug`
struct UnPrintable(i32);

// O atributo `derive` automaticamente implementa o `trait` `fmt::Debug`.
#[derive(Debug)]
struct DebugPrintable(i32);
```

Todos tipos da biblioteca padrao sao printaveis com `{:?}`:

```rust,editable
// Derive a implementacao de `fmt::Debug` para `Structure`. `Structure`
// é uma estrutura que contem um único `i32`.
#[derive(Debug)]
struct Structure(i32);

// Coloque a estrutura `Structure` dentro da estrutura `Deep`. Torne-a printavel
#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // Printando com `{:?}` é similar a `{}`.
    println!("{:?} mes em um ano.", 12);
    println!("{1:?} {0:?} é o nome {actor:?}.",
             "Slater",
             "Christian",
             actor="ator");

    // `Structure` é printavel!
    println!("Agora {:?} vai printar!", Structure(3));
    
    // O problema com `derive` é que nao é possível controlar
    // o resultado. Como faco para apenas mostrar `7`?
    println!("Agora {:?} vai printar!", Deep(Structure(7)));
}
```

`fmt::Debug` definitivamente faz isso ser printavel sacrificando elegancia.
Rust também fornece "pretty printing" com `{:#?}`.

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // Pretty print
    println!("{:#?}", peter);
}
```

`fmt::Display` pode ser implementado para controlar a forma que a informacao é mostrada.

### Veja também:

[atributos][attributes], [`derive`][derive], [`std::fmt`][fmt],
e [`estruturas`][structs]

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: ../../custom_types/structs.md

