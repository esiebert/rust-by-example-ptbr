# Arrays e Fatias

Um array é uma colecao de objetos do mesmo tipo `T`, armazenados em memória contígua.
Arrays sao criados usando colchetes `[]`, e seu tamanho, que é conhecido em tempo de
compilacao, é parte da assinatura `[T; tamanho]`.

Fatias sao similares à arrays, mas seu tamanho nao é conhecido em tempo de compilacao.
Uma fatia é um objeto de duas palavras, a primeira palavra é um ponteira para o dado,
e a segunda paavra é o tamanho da fatia. O tamanho da palavra é o mesmo de um usize,
determinado pela arquitetura do processador.
Fatias podem ser utilizados para pegar emprestado partes de um array, e tem a assinature de tipo 
`&[T]`.

```rust,editable,ignore,mdbook-runnable
use std::mem;

// Essa funcao pega uma fatia emprestada
fn analyze_slice(slice: &[i32]) {
    println!("primeiro elemento da fatia: {}", slice[0]);
    println!("a fatia tem {} elementos", slice.len());
}

fn main() {
    // Array de tamanho fixo (assinatura de tipo é superfluo)
    let xs: [i32; 5] = [1, 2, 3, 4, 5];

    // Todos elementos podem ser inicializados com o mesmo valor
    let ys: [i32; 500] = [0; 500];

    // Indices comecam em 0
    println!("primeiro elemento do array: {}", xs[0]);
    println!("segundo elemento do array: {}", xs[1]);

    // `len` retorna o tamanho do array
    println!("tamanho: {}", xs.len());

    // Arrays sao alocados na stack
    println!("array ocupa {} bytes", mem::size_of_val(&xs));

    // Arrays podem ser emprestados automaticamente como fatias
    println!("Emprestar o array inteiro como fatia");
    analyze_slice(&xs);

    // Fatias apontam para seccoes em um array
    // Eles tem forma [indice_inicial..indice_final]
    // indice_inicial é a primeira posicao da fatia
    // indice_final é um a mais que a posicao final da fatia
    println!("Emprestar uma seccao do array como fatia");
    analyze_slice(&ys[1 .. 4]);

    // Indices fora do limite causam erros de compilacao
    println!("{}", xs[5]);
}
```
