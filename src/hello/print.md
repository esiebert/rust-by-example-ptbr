# Print formatado

Print é tratado por uma série de [`macros`][macros] definidos em [`std::fmt`][fmt]
dos quais incluem:

* `format!`: escreve texto formatado em uma [`String`][string]
* `print!`: como `format!` mas é printado no console (io::stdout).
* `println!`: como `print!` mas uma nova linha é adicionada.
* `eprint!`: como `format!` mas o texto é escrito ao standard error (io::stderr).
* `eprintln!`: como `eprint!` mas uma nova linha é adicionada.

Todos analisam o texto da mesma forma. Como bonus, Rust verifica formatacao 
correta em tempo de compilacao.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Em geral, o `{}` será automáticamente substituido por qualquer argumento
    // Esses viram strings.
    println!("{} dias", 31);

    // Sem sufixo, 31 se torna i32. Voce pode trocar o tipo de 31 
    // adicionando um sufixo.

    // Existem vários padroes opcionais, um deles sendo o posicional
    // arguments can be used.
    println!("{0}, esse e {1}. {1}, esse e {0}", "Alice", "Bob");

    // argumentos nomeados.
    println!("{sujeito} {verbo} {objeto}",
             objeto="the lazy dog",
             sujeito="the quick brown fox",
             verbo="jumps over");

    // Formatacao especial pode ser especificada com `:`.
    println!("{} de {:b} pessoas sabem de binario, a outra metade nao", 1, 2);

    // Voce pode justificar o texto a direita com um comprimento definido. 
    // O output disso será
    // "     1". 5 espaco vazios e "1".
    println!("{number:>width$}", number=1, width=6);

    // Voce pode adicionar zeros extras. O output será "000001".
    println!("{number:>0width$}", number=1, width=6);

    // Rust verifica até se o número correto de argumentos é passado.
    println!("My name is {0}, {1} {0}", "Bond");
    // FIXME ^ Adicione o argumento faltante: "James"

    // Cria uma estrutura chamada `Structure` que contem um `i32`.
    #[allow(dead_code)]
    struct Structure(i32);

    // Porém, tipos customizados como este exigem tratamento mais complicado.
    // Isso nao funcionará.
    println!("This struct `{}` won't print...", Structure(3));
    // FIXME ^ Comente esta linha.
}
```

[`std::fmt`][fmt] contém vários [`traits`][traits] que governam o display de textos.
A forma básica de dois dos mais importantes é listado abaixo:

* `fmt::Debug`: Usa o marcador `{:?}`. Formata texto para motivos de debug.
* `fmt::Display`: Usa o marcador `{}`. Formata texto de forma mais elegante e amigável
ao usuário.

Aqui, usamos `fmt::Display` porque a biblioteca padrao possui implementacoes 
para estes tipos. Para printar textos de tipos customizados, mais passos sao necessários.

Implementar o trait `fmt::Display` automaticamente implementa o trait
[`ToString`] que nos permite [converter][convert] o tipo para [`String`][string].

### Actividades

 * Conserte os dois problemas no código acima (veja FIXME) para que rode sem erros.
 * Inclua um `println!` que printa: `Pi is roughly 3.142` controlando
   o número de casas decimais. Para este exercício, use `let pi = 3.142592`
   como estimativa de pi. (Dica: voce talvez precise verficiar a documentacao de
   [`std::fmt`][fmt] para especificar o numero de casas decimais)

### Veja também:

[`std::fmt`][fmt], [`macros`][macros], [`struct`][structs],
and [`traits`][traits]

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: ../trait.md
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convert]: ../conversion/string.md
