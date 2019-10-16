# Enumeracoes C

`enum` também pode ser usado como uma enumeracao similar a C.

```rust,editable
// Um atributo para esconder avisos de código inutilizado.
#![allow(dead_code)]

// enum com discriminantes implicitos (comecando em 0)
enum Numeros {
    Zero,
    Um,
    Dois,
}

// enum com discriminante explicito
enum Cor {
    Vermelho = 0xff0000,
    Verde = 0x00ff00,
    Azul = 0x0000ff,
}

fn main() {
    // `enums` podem ser convertidos a inteiros.
    println!("zero é {}", Numero::Zero as i32);
    println!("um é {}", Numero::Um as i32);

    println!("Rosas sao #{:06x}", Cor::Vermelho as i32);
    println!("Violetas sao #{:06x}", Cor::Azul as i32);
}
```

### Veja também:

[conversao][cast]

[cast]: ../../types/cast.md
