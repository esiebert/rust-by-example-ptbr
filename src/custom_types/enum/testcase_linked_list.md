# Caso de teste: listas encadeadas

Um uso comum para `enums` é a criacao de listas encadeadas:

```rust,editable
use crate::List::*;

enum List {
    // Cons: Tupla estrutura que empacota um elemento e um ponteiro para o próximo nó
    Cons(u32, Box<List>),
    // Nil: Um nó significando o fim da lista encadeada
    Nil,
}

// Metodos podem ser anexados à uma enumeracao
impl List {
    // Cria lista vazia
    fn new() -> List {
        // `Nil` tem tipo `List`
        Nil
    }

    // Consome uma lista, e retorna a mesma lista com um novo elemento à sua frente
    fn prepend(self, elem: u32) -> List {
        // `Cons` também tem tipo List
        Cons(elem, Box::new(self))
    }

    // Retorna o tamanho da lista
    fn len(&self) -> u32 {
        // `self` precisa ser igualado, pois o comportamento deste método depente
        // na variante de `self`
        // `self` tem tipo `&List`, e `*self` tem tipo `List`, corresponder a um
        // tipo concreto `T` é preferível sobre correspondencia à uma referência `&T`
        match *self {
            // Nao é possível obter posse sobre a cauda, pois `self` é emprestado;
            // em vez disso, pega a referência da cauda
            Cons(_, ref tail) => 1 + tail.len(),
            // Caso base: Uma lista vazio possui tamanho zero
            Nil => 0
        }
    }

    // Retorna a representacao da lista como uma (alocada na heap) string
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // `format!` é similar à `print!`, porém retorna uma string
                // alocada na heap em vez de printar no console
                format!("{}, {}", head, tail.stringify())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // Cria lista encadeada vazia
    let mut list = List::new();

    // Adiciona alguns elementos
    list = list.prepend(1);
    list = list.prepend(2);
    list = list.prepend(3);

    // Mostra o estado final da lista
    println!("lista encadeada tem tamanho: {}", list.len());
    println!("{}", list.stringify());
}
```

### Veja também:

[`Box`][box] e [metodos][methods]

[box]: ../../std/box.md
[methods]: ../../fn/methods.md
