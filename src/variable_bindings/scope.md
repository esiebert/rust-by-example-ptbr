# Escopo e Sombreamento

Vínculos de variável possuem um escopo, e sao restringídas a viverem em um *bloco*.
Um bloco é uma colecao de comandos dentro de chaves `{}`. Sombreamento de variável é
permitido.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Esse vínculo vive na funcao main
    let vinculo_longa_vida = 1;

    // Isto é um bloco, e tem um escopo menor do que a funcao principal
    {
        // Este vínculo existe apenas nesse bloco
        let vinculo_curta_vida = 2;

        println!("curto dentro: {}", vinculo_curta_vida);

        // Este vínculo *sombrea* o de fora
        let vinculo_longa_vida = 5_f32;

        println!("longo dentro: {}", vinculo_longa_vida);
    }
    // Fim de bloco

    // Erro! `vinculo_curta_vida` nao existe nesse escopo
    println!("curto fora: {}", vinculo_vida_curta);
    // FIXME ^ Comente essa linha

    println!("longo fora: {}", vinculo_longa_vida);
    
    // Este vínculo também *sombrea* o último vínculo
    let vinculo_longa_vida = 'a';
    
    println!("longo fora: {}", vinculo_longa_vida);
}
```
