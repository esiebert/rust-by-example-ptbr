# Enumeracoes

A palavra-chave `enum` permite a criacao de um tipo que pode ser um de variantes diferentes.
Qualquer variante que é valida como um `struct`  também é valido como um `enum`.

```rust,editable
// Cria um `enum` para classificar eventos web. Note como ambos os nomes
// e tipo de informacao especificam uma variante:
// `PageLoad != PageUnload` e `KeyPress(char) != Paste(String)`.
// Cada um é diferente e independente.
enum WebEvent {
    // Um `enum` pode ou ser único,
    PageLoad,
    PageUnload,
    // como estrutura,
    KeyPress(char),
    Paste(String),
    // ou como estrutura C.
    Click { x: i64, y: i64 },
}

// Uma funcao que toma uma enumeracao `WebEvent` como argumento e retorna nada.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("Página carreada"),
        WebEvent::PageUnload => println!("Página descarregada"),
        // Desestrutura `c` de dentro do `enum`.
        WebEvent::KeyPress(c) => println!("pressionado '{}'.", c),
        WebEvent::Paste(s) => println!("colado \"{}\".", s),
        // Desestrutura `Click` em `x` e `y`.
        WebEvent::Click { x, y } => {
            println!("clicado em x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()` apropria-se de um `String` a partir de um fatia de string.
    let pasted  = WebEvent::Paste("meu testo".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}

```

## Apelidando tipos

Se voce usar apelidos para tipos, voce pode se referir à uma variante de enumeracao pelo seu apelido.
Isso pode ser útil se o nome de uma variante é muito longa ou genérica.

```rust,editable
enum EnumeracaoBemVerbosaParaCoisasENumeros {
    Adicionar,
    Subtrair,
}

// Cria um apelido para uma variante
type Operacoes = EnumeracaoBemVerbosaParaCoisasENumeros;

fn main() {
    // Agora, podemos nos referir as variantes pelo apelido, nao pelo nome comprido e inconveniente
    // name.
    let x = Operacoes::Adicionar;
}
```

O lugar mais comum para se ver isso é em blocos de `impl` usando o apelido `Self`.

```rust,editable
enum EnumeracaoBemVerbosaParaCoisasENumeros {
    Adicionar,
    Subtrair,
}

impl EnumeracaoBemVerbosaParaCoisasENumeros {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Adicionar => x + y,
            Self::Subtrair => x - y,
        }
    }
}
```

Para aprender mais sobre enumeracoes e apelidos, voce pode ler o
[relatório de estabilizacao][aliasreport] de quando este recurso foi estabilizado em Rust.

### Veja também:

[`match`][match], [`fn`][fn], e [`String`][str], ["Type alias enum variants" RFC][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html
