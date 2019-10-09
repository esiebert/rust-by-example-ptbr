# Primitivos

Rust fornece acesso a uma grande variadade de `primitivos`. Uma parte inclui:


### Tipos escalares 

* inteiros assinados: `i8`, `i16`, `i32`, `i64`, `i128` e `isize` (tamanho de ponteiro)
* inteiros nao-assinados: `u8`, `u16`, `u32`, `u64`, `u128` and `usize` (tamanho de ponteiro)
* ponto flutuante: `f32`, `f64`
* `char` valores escalares Unicode como `'a'`, `'α'` e `'∞'` (4 bytes cada)
* `bool` `true` ou `false`
* e o tipo unidade `()`, cujo único valor possível é uma tupla vazia: `()`

Apesar do valor de um tipo unidade ser uma tupla, nao é considera um tipo composto
pois nao possui multiplos valores.

### Tipos compostos

* arrays como `[1, 2, 3]`
* tuplas como `(1, true)`

Variáveis podem sempre ser *anotados com tipo*. Números podem adicionalmente ser
anotados com um *sufixo* ou *por default*. Inteiros tem default como `i32` e
floats como `f64`. Note que Rust também consegue inferir tipos atráves do contexto.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Variáveis podem ser anotadas com tipo.
    let logical: bool = true;

    let a_float: f64 = 1.0;  // Anotacao normal
    let an_integer   = 5i32; // Anotacao por sufixo

    // Ou um tipo default é usado.
    let default_float   = 3.0; // `f64`
    let default_integer = 7;   // `i32`
    
    // Tipos podem ser inferidos pelo contexto 
    let mut inferred_type = 12; // Tipo i64 é inferrido a partir de outra linha
    inferred_type = 4294967296i64;
    
    // O valor de uma variável mutável pode ser alterada.
    let mut mutable = 12; // Mutable `i32`
    mutable = 21;
    
    // Erro! O tipo de uma variável nao pode ser alterada.
    mutable = true;
    
    // Variáveis podem ser sobrescrevidas com shadowing.
    let mutable = true;
}
```

### Veja também:

[a biblioteca `std`][std], [`mut`][mut], [inferencia], e [shadowing]

[std]: https://doc.rust-lang.org/std/
[mut]: variable_bindings/mut.md
[inferencia]: types/inference.md
[shadowing]: variable_bindings/scope.md
