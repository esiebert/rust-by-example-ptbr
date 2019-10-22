# Inferência

O mecanismo de inferência de tipo é bem esperto. Ele faz mais do que apenas olhar
o tipo do valor na inicializacao.
Ele também olha como a variável é utilizada mais tarde para inferir seu tipo.
Aqui está um exemplo avancado de inferência de tipo:

```rust,editable
fn main() {
    // Por causa da anotacao, o compilador sabe que `elem` tem tipo u8.
    let elem = 5u8;

    // Cria um vetor vazio (um array que cresce).
    let mut vec = Vec::new();
    // Nesse ponto, o compilador nao sabe o exato tipo de `vec`, ele
    // só sabe que é um vetor de alguma coisa (`Vec<_>`).

    // Insere `elem` no vetor.
    vec.push(elem);
    // Aha! Agora o compilador sabe que `vec` é um vetor de `u8`s (`Vec<u8>`)
    // TODO ^ Comente a linha com `vec.push(elem)`

    println!("{:?}", vec);
}
```

Nenhuma anotacao de variável foi necessário, o compilador está feliz assim como o programador!
