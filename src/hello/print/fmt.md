# Formatacao

Nós vimos que formatacao é especificado através de um *string de formatacao*:

* `format!("{}", foo)` -> `"3735928559"`
* `format!("0x{:X}", foo)` ->
  [`"0xDEADBEEF"`][deadbeef]
* `format!("0o{:o}", foo)` -> `"0o33653337357"`

A mesma variável (`foo`) pode ser formatada de forma diferente dependendo de qual
*tipo de argumento* é usado: `X` vs `o` vs *nao especificado*.

A funcionalitade de formatacao é implementada através de traits, e existe um trait 
para cada tipo de argumento. O trait mais comum é o `Display`, que lida com casos
onde o tipo de argumento nao é especificado: `{}` por exemplo.

```rust,editable
use std::fmt::{self, Formatter, Display};

struct Cidade {
    nome: &'static str,
    // Latitude
    lat: f32,
    // Longitude
    lon: f32,
}

impl Display for Cidade {
    // `f` é um buffer, e este método escreve o string formatado dentro do buffer
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'L' } else { 'O' };

        // `write!` é como `format!`, mas escrever o string formatado
        // no buffer (o primeiro argumento)
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.nome, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

#[derive(Debug)]
struct Cor {
    red: u8,
    green: u8,
    blue: u8,
}

fn main() {
    for cidade in [
        Cidade { nome: "Sao Paulo", lat: -10.347778, lon: -16.259722 },
        Cidade { nome: "Brasilia", lat: 59.95, lon: 10.75 },
        Cidade { nome: "Curitiba", lat: -30.25, lon: -1.1 },
    ].iter() {
        println!("{}", *cidade);
    }
    for cor in [
        Cor { red: 128, green: 255, blue: 90 },
        Cor { red: 0, green: 3, blue: 254 },
        Cor { red: 0, green: 0, blue: 0 },
    ].iter() {
        // Troque isso por {} quando tiver implementado fmt::Display.
        println!("{:?}", *cor);
    }
}
```

Você pode ver a [lista completa de traits de formatacao][fmt_traits] e seus tipos de argumentos
na documentacao de [`std::fmt`][fmt].

### Atividade
Adicione a implementacao do trait `fmt::Display` para a estrutura `Cor` acima
para que o output seja como o seguinte:

```text
RGB (128, 255, 90) 0x80FF5A
RGB (0, 3, 254) 0x0003FE
RGB (0, 0, 0) 0x000000
```

Duas dicas, caso esteja preso:
 * Voce [pode precisar listar cada cor mais de uma vez][named_parameters],
 * Voce pode [preencher com zeros com comprimento de 2][fmt_width] com `:02`.

### Veja também:

[`std::fmt`][fmt]

[named_parameters]: https://doc.rust-lang.org/std/fmt/#named-parameters
[deadbeef]: https://en.wikipedia.org/wiki/Deadbeef#Magic_debug_values
[fmt]: https://doc.rust-lang.org/std/fmt/
[fmt_traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[fmt_width]: https://doc.rust-lang.org/std/fmt/#width
