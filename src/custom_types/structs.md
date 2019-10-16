# Estruturas

Existem 3 tipos de estruturas ("structs") que podem ser criados usando a palavra-chave `struct`.

* Tuplas estruturas, que sao basicamente tuplas com nome.
* As clássicas [estruturas C][c_struct]
* Estruturas de unidade, que nao possuem campos, sao úteis para genéricos.

```rust,editable
#[derive(Debug)]
struct Pessoa<'a> {
    // O 'a define o tempo de vida
    nome: &'a str,
    idade: u8,
}

// Uma estrutura unidade
struct Nil;

// Uma tupla estrutura
struct Pair(i32, f32);

// Estrutura com dois campos
struct Point {
    x: f32,
    y: f32,
}

// Estruturas podem ser reusadas como campos em outras estruturas
#[allow(dead_code)]
struct Rectangle {
    // Um retângulo pode ser especificado pelas coordenadas do canto superior esquerdo e inferior direito.
    sup_esq: Point,
    inf_dir: Point,
}

fn main() {
    // Criar estrutura
    let nome = "Pedro";
    let idade = 27;
    let pedro = Pessoa { nome, idade };

    // Printar estrutura com debug
    println!("{:?}", peter);


    // Instanciar um `Point`
    let point: Point = Point { x: 10.3, y: 0.4 };

    // Acessar os campos do ponto
    println!("coordenadas do ponto: ({}, {})", point.x, point.y);

    // Cria um novo ponto usando sintaxe de update de estruturas usando o valor do ponto criado anteriormente
    let bottom_right = Point { x: 5.2, ..point };

    // `inf_dir.y` será o mesmo que `point.y` porque usamos este campo de `point`
    println!("segundo ponto: ({}, {})", inf_dir.x, inf_dir.y);

    // Desestruturar o ponto usando uma conexao `let`
    let Point { x: canto_sup, y: canto_esq } = point;

    let _rectangle = Rectangle {
        // instanciacao de estruturas também é uma expressao
        sup_esq: Point { x: canto_esq, y: canto_sup },
        inf_dir: inf_dir,
    };

    // Instaciacao de estrutura de unidade
    let _nil = Nil;

    // Instanciacao de tupla estrutura
    let pair = Pair(1, 0.1);

    // Acesso à campos de uma tupla estrutura
    println!("pair contém {:?} é {:?}", pair.0, pair.1);

    // Desestrutura uma tupla estrutura
    let Pair(integer, decimal) = pair;

    println!("pair contém {:?} e {:?}", integer, decimal);
}
```

### Atividade

1. Implemente a funcao `rect_area` que calcula a area do retângulo (tente usar desestruturacao aninhada)
2. Implemente a funcao `square` que toma um `Point` e um `f32` como argumento, e retorna um `Rectangle` com seu canto inferior esquerda
no ponto, e uma largura e altura correspondente ao `f32`.

### Veja também:

[`atributos`][attributes], [tempo de vida][lifetime] e [desestruturacao][destructuring]

[attributes]: ../attribute.md
[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[destructuring]: ../flow_control/match/destructuring.md
[lifetime]: ../scope/lifetime.md
