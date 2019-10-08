# Display

`fmt::Debug` esta longe de ser compacto e limpo, entao é vantajoso customizar
a aparencia do output. Isso é possível através da implementacao manual de
[`fmt::Display`][fmt], que usa o marcador `{}`. A implementacao exemplo é
a seguinte:

```rust
// Importe (via `use`) o modulo `fmt` para que esteja disponível.
use std::fmt;

// Defina uma estrutura para qual será implementado o `fmt::Display`. Isso é
// um estrutura tupla chamada `Structure` que contem um `i32`.
struct Structure(i32);

// Para usar o marcador `{}`, o trait `fmt::Display` deve ser implementado manualmente.
impl fmt::Display for Structure {
    // Este trait necessita de `fmt` come esta exata assinatura.
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Escreve o primeiro elemento dentro do strem de output `f`
        // Retorna `fmt::Result` que indica se a operacao sucediu ou falhou.
        // Note que `write!` usa sintaxe similar a `println!`.
        write!(f, "{}", self.0)
    }
}
```

`fmt::Display` pode ser mais limpo que `fmt::Debug` mas isso é um problema
para a biblioteca padrao. Como devem ser mostrados tipos ambiguos?
Por exemplo, se a biblioteca `std` implementa um único estilo para todos os
`Vec<T>`, que estilo deve ser adotado? Seria um destes dois?

* `Vec<caminho>`: `/:/etc:/home/username:/bin` (divide em `:`)
* `Vec<numero>`: `1,2,3` (divide em `,`)

Nao, porque nao há estilo ideal para todos os tipos e a biblioteca padrao nao
dita qual delas é escolhida. `fmt::Display` nao é implementado para `Vec<T>`
ou para qualquer container genérico. `fmt::Debug` deve ser usado para estes casos genéricos.

Isso nao é problema, pois para cada novo *container* que *nao* é genérico,
,`fmt::Display` pode ser implementado.

```rust,editable
use std::fmt; // Import `fmt`

// Uma estrutura contendo 2 numeros. `Debug` será derivado para que o resultado
// seja comparado com o resultado de `Display`.
#[derive(Debug)]
struct MinMax(i64, i64);

// Implementa `Display` para `MinMax`.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Use `self.number` para se referir aos dados posicionais.
        write!(f, "({}, {})", self.0, self.1)
    }
}

// Define uma estrutura onde os campos sao nomeaveis para comparacao.
#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// Implemente `Display` para `Point2D`
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Customize para que apenas `x` e `y` sao mostrados.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("Comparacao de estruturas:");
    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let limite_superior =   MinMax(-300, 300);
    let limite_inferior = MinMax(-3, 3);

    println!("O limite superior é {superior} e o inferior é {inferior}",
             inferior = limite_inferior,
             superior = limiute_superior);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("Comparacao de pontos:");
    println!("Display: {}", point);
    println!("Debug: {:?}", point);

    // Erro. Amobs `Debug` e `Display` foram implementados, porém `{:b}`
    // necessita da implementacao de `fmt::Binary`. Isso nao funcionará.
    // println!("Como Point2D parece em binário: {:b}?", point);
}
```

`fmt::Display` foi implementado, porém nao `fmt::Binary`, e entao nao
pode ser usado. `std::fmt` possui muitos [`traits`][traits] e cada um
exige sua própria implementacao. Mais detalhes em [`std::fmt`][fmt].

### Atividade

Depois de verificar o output do exemplo acima, use a estrutura `Point2D` para
adicionar a estrutura Complexo ao exemplo. Quando printado do mesmo jeito,
o output deve parecer com o seguinte:

```txt
Display: 3.3 + 7.2i
Debug: Complexo { real: 3.3, imag: 7.2 }
```

### Veja também:

[`derive`][derive], [`std::fmt`][fmt], [macros], [`estruturas`][structs],
[`trait`][traits], e [use][use]

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: ../../trait.md
[use]: ../../mod/use.md
