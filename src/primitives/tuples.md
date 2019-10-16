# Tuplas

Uma tupla é uma colecao de valores de tipos diferentes. Tuplas sao construidas
usando parenteses `()`, e cada tupla é um valor com assinatura de tipo
`(T1, T2, ...)`, onde `T1`, `T2` sao os tipos dos membros. Funcoes podem
usar tuplas para retornar multiplos valores visto que tuplas podem conter quantos valores
forem necessários.

```rust,editable
// Tuplas podem ser usadas como argumentos de funcao e como valores de retorno
fn reverse(pair: (i32, bool)) -> (bool, i32) {
    // `let` pode ser usado para conectar membros de uma tupla à variáveis
    let (integer, boolean) = pair;

    (boolean, integer)
}

// A estrutura abaixo é para a atividade.
#[derive(Debug)]
struct Matrix(f32, f32, f32, f32);

fn main() {
    // Uma tupla com diversos tipos diferentes
    let long_tuple = (1u8, 2u16, 3u32, 4u64,
                      -1i8, -2i16, -3i32, -4i64,
                      0.1f32, 0.2f64,
                      'a', true);

    // Valores podem ser extraídos de tuplas usando índices
    println!("long tuple primeiro valor: {}", long_tuple.0);
    println!("long tuple segundo valor: {}", long_tuple.1);

    // Tuplas podem ser membros de tuplas
    let tuple_of_tuples = ((1u8, 2u16, 2u32), (4u64, -1i8), -2i16);

    // Tuplas sao printáveis
    println!("Tupla de tuplas: {:?}", tuple_of_tuples);
    
    // Mas tuplas longas nao sao printáveis
    // let too_long_tuple = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13);
    // println!("tupla muito longa: {:?}", too_long_tuple);
    // TODO ^ Descomente as 2 linhas acima para ver o erro de compilacao

    let pair = (1, true);
    println!("pair é {:?}", pair);

    println!("o pair reverso é {:?}", reverse(pair));

    // Para criar uma tupla de um único elemento, o uso da vírgula é necessário para diferenciar
    // a tupla de um literal rodeado por parenteses
    println!("Tupla de um elemento: {:?}", (5u32,));
    println!("Apenas um inteiro: {:?}", (5u32));

    // Tuplas podem ser destruídas para criar conexoes
    let tuple = (1, "hello", 4.5, true);

    let (a, b, c, d) = tuple;
    println!("{:?}, {:?}, {:?}, {:?}", a, b, c, d);

    let matrix = Matrix(1.1, 1.2, 2.1, 2.2);
    println!("{:?}", matrix);

}
```

### Atividade

 1. *Recapitulando*: Implemente o trait `fmt::Display` para a estrutura Matrix no exemplo acima
    para que, quando trocado a formatacao do print de `{:?}` para `{}`, o output seja o seguinte:

    ```text
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    ```

    Você pode precisar olhar o exemplo para [printar display][print_display].
 2. Implemente a funcao `transposta` usando a funcao `reverse` como template, que
    aceita uma matrix como argumento, e retorna uma matrix onde dois elementos
    foram trocados. Por exemplo:

    ```rust,ignore
    println!("Matrix:\n{}", matrix);
    println!("Transposta:\n{}", transpose(matrix));
    ```

    Output:

    ```text
    Matrix:
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    Transposta:
    ( 1.1 2.1 )
    ( 1.2 2.2 )
    ```

[print_display]: ../hello/print/print_display.md
