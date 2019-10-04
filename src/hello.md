# Hello World

Este é o código do tradicional programa Hello World.

```rust,editable
// Isto é um comentário, ignorado pelo compilador
// Voce pode testar o código clicando em "Run" logo ali ->
// ou se prefirir usar o teclado, use o shortcut "Ctrl + Enter"

// O código é editável, sinta-se livre para hackear!
// Voce pode sempre voltar ao código original clicando no botao "Reset" ->

// Essa é a funcao principal
fn main() {
    // Declaracoes sao chamadas quando o binários compilado é chamado

    // Printa texto no console
    println!("Hello World!");
}
```

`println!` é um [*macro*][macros] que printa texto no
console.

Um binário pode ser gerado usando o compilador Rust: `rustc`.

```bash
$ rustc hello.rs
```

`rustc` produz o binário `hello` que pode ser executado.

```bash
$ ./hello
Hello World!
```

### Atividade

Clique 'Run' acima para ver o output esperado. Agora, adicione
um segundo `println!` macro para que o output seja como:

```text
Hello World!
Eu sou um Rustacean!
```

[macros]: macros.md
