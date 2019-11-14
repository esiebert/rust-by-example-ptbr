# De e para Strings

## Convertendo para String

Converter qualquer tipo para `String` é tao simples como implementar o trait [`ToString`]
para o tipo. Invés de fazer isso diretamente, você deve implementar o trait
[`fmt::Display`][Display] que automagicamente fornece [`ToString`] e
também permite printar o tipo como discutido na seccao [`print!`][print].

```rust,editable
use std::fmt;

struct Circulo {
    raio: i32
}

impl fmt::Display for Circulo {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "Circulo com raio {}", self.raio)
    }
}

fn main() {
    let circulo = Circulo { raio: 6 };
    println!("{}", circulo.to_string());
}
```

## Fazendo parsing de uma String

Um dos jeitos mais comuns de converter uma string em um número. A forma idiomatica
de fazer isso é usando a funcao [`parse`] e fornecer o tipo desejado para a funcao
que ira transformar a string para este tipo. Isso pode ser feito ou sem inferência
de tipo ou usando a sintaxe 'turbofish'.

Isso ira converter a string ao tipo especificado contanto que o trait [`FromStr`]
tenha sido implementado. Isso é implementado para diversos tipos na biblioteca padrao.
Para obter essa funcionalidade em um tipo customizado, simplesmente implemente o trait
[`FromStr`] para aquele tipo.

```rust,editable
fn main() {
    let parsed: i32 = "5".parse().unwrap();
    let turbo_parsed = "10".parse::<i32>().unwrap();

    let soma = parsed + turbo_parsed;
    println!("Soma: {:?}", sum);
}
```

[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[Display]: https://doc.rust-lang.org/std/fmt/trait.Display.html
[print]: ../hello/print.md
[`parse`]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[`FromStr`]: https://doc.rust-lang.org/std/str/trait.FromStr.html
