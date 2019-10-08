# Caso de teste: Lista

Implementar `fmt::Display` para uma estrutura onde os elementos precisam ser tratados
de forma sequencial é complicado. O problema é que cada `write!` gera um `fmt::Result`.
Tratamento correto dessa estrutura exige lidar com *todos* os resultados.
Rust fornece o operador `?` especialmente para esse caso.

O uso de `?` em `write!` é feito da seguinte forma:

```rust,ignore
// Tente executar `write!` para ver se causa erros. se causar erros, retorne o erro.
// Caso contrário, continue.
write!(f, "{}", value)?;
```

De outra forma, a macro `try!` também pode ser usada, que funciona da mesma forma. 
Esse é um pouco mais verboso e nao mais recomendado, mas isso ainda pode ser achado
em códigos Rust antigos. O uso de `try!` segue:

```rust,ignore
try!(write!(f, "{}", value));
```

Com `?` disponível, implementar `fmt::Display` para um `Vec` é direto:

```rust,editable
use std::fmt; // Importa o módulo `fmt`.

// Define uma estrutura chamada `List` contendo um `Vec`.
struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Extrai o valor usando indexacao de tuplas,
        // e cria uma referencia para `vec`.
        let vec = &self.0;

        write!(f, "[")?;

        // Itera sobre `v` em `vec` enquanto enumera o contador `count`.
        for (count, v) in vec.iter().enumerate() {
            // Para cada elemento, exceto o primeiro, adiciona uma vírgula.
            // Usa o operador ?, ou try!, para retornar erros.
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }

        // Fecha o colchete aberto e retorna um valor fmt::Result.
        write!(f, "]")
    }
}

fn main() {
    let v = List(vec![1, 2, 3]);
    println!("{}", v);
}
```

### Atividade

Tente mudar o programa para que o indice de cada elemento no vetor também é printado.
O output deve parecer como o seguinte:

```rust,ignore
[0: 1, 1: 2, 2: 3]
```

### Veja também:

[`for`][for], [`ref`][ref], [`Result`][result], [`estrutura`][struct],
[`?`][q_mark], e [`vec!`][vec]

[for]: ../../../flow_control/for.md
[result]: ../../../std/result.md
[ref]: ../../../scope/borrow/ref.md
[struct]: ../../../custom_types/structs.md
[q_mark]: ../../../std/result/question_mark.md
[vec]: ../../../std/vec.md
