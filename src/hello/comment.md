# Comentários

Qualquer programa necessita comentários, e Rust
suporta algumas variedades de comentários:
Any program requires comments, and Rust supports
a few different varieties:

* *Comentários normais* que sao ignorados pelo compilador:
   * `// Comentário que vao até o final da linha.`
   * `/* Comentários de bloco que vao até o delimitador. */`
* *Comentários de documentacao* que sao traduzidos para uma [documentacao][docs] HTML:
   * `/// Gera documentacao para o item seguinte.`
   * `//! Gera documentacao para o item no qual esta contido.`

```rust,editable
fn main() {
    // Exemplo de comentário de linha
    // Há 2 barras no comeco da linha
    // E nada dentro é lido pelo compilador

    // println!("Hello, world!");

    // Execute. Viu? Agora delete as barras e execute de novo.

    /* 
     * Esse é o comentário de bloco. Em gerag, comentários de linha
     * é o estilo recomendado, porém comentários de bloco sao úteis
     * para desabilitar pedacos de código.
     /* Comentário de bloco podem estar /* aninhados, */ */
     * entao leva apenas alguns caracteres para comentar tudo
     * nessa funcao main(). /*/*/* Tente voce mesmo! */*/*/
     */

    // Voce pode manipular expressoes mais facilmente com comentários de bloco
    // do que com comentários de linha. Delete os delimitadores e mude o resultado:
    let x = 5 + /* 90 + */ 5;
    println!("`x` e 10 ou 100? x = {}", x);
}

```

### Veja também:

[Biblioteca de documentacao][docs]

[docs]: ../meta/doc.md
