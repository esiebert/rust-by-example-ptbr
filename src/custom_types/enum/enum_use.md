# use

A declaracao `use` pode ser usada para que escopo manual nao seja necessário:

```rust,editable
// Um atributo para esconder avisos de código inutilizado.
#![allow(dead_code)]

enum Status {
    Rico,
    Pobre,
}

enum Trabalho {
    Civil,
    Soldado,
}

fn main() {
    // Explicitamete `use` cada nome para que sejam disponíveis sem escopo manual.
    use crate::Status::{Pobre, Rico};
    // Automaticamente `use` cada nome dentro de `Trabalho`.
    use crate::Trabalho::*;

    // Equivalente à `Status::Pobre`.
    let status = Pobre;
    // Equivalente à `Trabalho::Civil`.
    let trabalho = Civil;

    match status {
        // Note a falta de escopo por causa do `use` acima.
        Rico => println!("Os ricos tem muito dinheiro!"),
        Pobre => println!("Os pobres nao tem dinheiro..."),
    }

    match trabalho {
        // Note de novo a falta de escopo.
        Civil => println!("Civis trabalham!"),
        Soldado  => println!("Soldados lutam!"),
    }
}
```

### Veja também:

[`match`][match] e [`use`][use] 

[use]: ../../mod/use.md
[match]: ../../flow_control/match.md
