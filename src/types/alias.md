# Apelidos (Alias)

A declaracao `type` pode ser usada para dar um novo nome a um tipo já existente.
Tipos devem ter nome `CamelCase`, ou o compilador levanta uma alerta. A excecao para
esta regra sao os tipos primitivos: `usize`, `f32`, etc.

```rust,editable
// `NanoSegundo` é um novo nome para `u64`.
type NanoSegundo = u64;
type Centimetro = u64;

// Uso de um atributo para silenciar alertas.
#[allow(non_camel_case_types)]
type u64_t = u64;
// TODO ^ Tente remover o atributo

fn main() {
    // `NanoSegundo` = `Centimetro` = `u64_t` = `u64`.
    let nanosegundos: NanoSegundo = 5 as u64_t;
    let centimetros: Centimetro = 2 as u64_t;

    // Note que apelidos *nao* fornecem seguranca extra de tipo, pois
    // apelidos *nao* sao novos tipos
    println!("{} nanosegundos + {} centimetros = {} unidade?",
             nanosegundos,
             centimetros,
             nanosegundos + centimetros);
}
```

O uso principal de alias é para reduzir nomes longos; por exemplo o tipo `IoResult<T>`
é uma apelido para o tipo `Result<T, IoError>`.

### Veja também:

[Atributos](../attribute.md)
