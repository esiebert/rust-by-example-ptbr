# Mutabilidade

Vínculos de variável sao imutáveis por padrao, porém isso pode ser alterado usando
o modificador `mut`.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let _vinculo_imutavel = 1;
    let mut vinculo_mutavel = 1;

    println!("Antes da mutacao: {}", vinculo_mutavel);

    // Ok
    vinculo_mutavel += 1;

    println!("Após mutacao: {}", vinculo_mutavel);

    // Erro!
    _vinculo_imutavel += 1;
    // FIXME ^ Comente essa linha
}
```

O compilador reporta um diagnóstico detalhado sobre erros de mutabilidade.
