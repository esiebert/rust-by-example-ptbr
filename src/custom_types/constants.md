# Constantes

Rust possui dois tipos diferentes de constantes que podem ser declaradas em qualquer escopo
incluido global. Ambos exigem explicita anotacao de tipo:

* `const`: Um valor fixo (caso comum).
* `static`: uma possível variável `mut`ável com tempo de vida [`'static`][static].
  O tempo de vida estático é inferido e nao precisa ser especificado.
  Acessar e modificar variáveis estáticas mutáveis é [`inseguro`][unsafe].

```rust,editable,ignore,mdbook-runnable
// Variáveis globais sao declaradas fora de qualquer escopo.
static LINGUAGEM: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    // Acessando constante em uma funcao
    n > THRESHOLD
}

fn main() {
    let n = 16;

    // Acessando constante dentro da main
    println!("Isso é {}", LINGUAGEM);
    println!("O threshold é {}", THRESHOLD);
    println!("{} é {}", n, if is_big(n) { "grande" } else { "pequeno" });

    // Erro! Nao é possível modificar uma `const`.
    THRESHOLD = 5;
    // FIXME ^ Comente esta linha
}
```

### Veja também:

[A RFC de `const`/`static`](
https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md),
[Tempo de vida `'static`][static]

[static]: ../scope/lifetime/static_lifetime.md
[unsafe]: ../unsafe.md
