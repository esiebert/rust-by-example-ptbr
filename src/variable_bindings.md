# Vinculacao de variáveis

Rust fornece seguranca de tipagem através de digitacao estática. Atribuicao de variáveis podem ser
anotadas com tipo quando declaradas. Porém, na maioria dos casos, o compilador consegue
inferir o tipo de uma variável a partir do contexto, reduzindo o trabalho da anotacao.

Valores (como literais) podem ser vinculados à uma variável, usando o vínculo `let`.

```rust,editable
fn main() {
    let um_inteiro = 1u32;
    let um_booleano = true;
    let unidade = ();

    // copia `um_inteiro` em `inteiro_copiado`
    let inteiro_copiado = um_inteiro;

    println!("Um inteiro: {:?}", inteiro_copiado);
    println!("A boolean: {:?}", um_booleano);
    println!("Conheca o valor de unidade: {:?}", unidade);

    // O compilador alerta sobre vínculos de variável inutilizados; esses alertas podem
    // ser silenciados prefixando um underscore
    let _variavel_inutilizada = 3u32;

    let variavel_inutilizada_barulhenta = 2u32;
    // FIXME ^ Adicione um underscore ao prefixo para silenciar o alerta
}
```
