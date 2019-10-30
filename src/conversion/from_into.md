# `From` e `Into`

Os traits [`From`] e [`Into`] sao linkados inerentemente, e isso faz parte
de sua implementacao. Se você pode converter do tipo A para tipo B, entao deve ser
fácil entender que deve ser possível converter de tipo B para tipo A.

## `From`

O trait [`From`] permite um tipo definir como se criar a partir de outro tipo,
e assim fornecendo um mecanismo simples de conversao entre diversos tipos.
Existem inúmeras implementacoes desse trait na biblioteca padrao para conversao
entre tipos comuns e primitivos.

Por exemplo, a conversao de um `str` para um `String`

```rust
let my_str = "hello";
let my_string = String::from(my_str);
```

Nós podemos fazer algo similar para um tipo próprio.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Numero {
    valor: i32,
}

impl From<i32> for Numero {
    fn from(item: i32) -> Self {
        Numero { valor: item }
    }
}

fn main() {
    let num = Numero::from(30);
    println!("Meu número é {:?}", num);
}
```

## `Into`

O trait [`Into`] é a forma reciproca do trait `From`. Isto é, se você tiver
implementado o trait `From` para seu tipo, você recebe a implementacao de `Into`
de graca.

O uso do trait `Into` tipicamente exige a especificacao do tipo a ser convertido
visto que o compilador é incapaz de determinar o tipo na maioria dos casos.
Porém, esta é uma pequena troca visto que recevemos a funcionalidade de graca.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Numero {
    valor: i32,
}

impl From<i32> for Numero {
    fn from(item: i32) -> Self {
        Numero { valor: item }
    }
}

fn main() {
    let int = 5;
    // Tente remover a declaracao do tipo
    let num: Numero = int.into();
    println!("Meu número é {:?}", num);
}
```

[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
