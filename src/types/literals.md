# Literais

Literais numéricos podem ser anotados com tipo adicionando um sufixo. Por exemplo, 
para especificar que `42` será de tipo `i32`, escreve se `42i32`.

O tipo de literais numéricos sem sufixo depende de como sao usados. Se nenhum restricao
existe, o compilador usa `i32` para inteiros, e `f64` para números flutuantes.

```rust,editable
fn main() {
    // Literais com sufixo. Seus tipos sao conhecidos na inicializacao
    let x = 1u8;
    let y = 2u32;
    let z = 3f32;

    // Literais sem sufixo. Seus tipos dependem de como sao usados
    let i = 1;
    let f = 1.0;

    // `size_of_val` retorna o tamanho da variável em bytes
    println!("tamanho de `x` em bytes: {}", std::mem::size_of_val(&x));
    println!("tamanho de `y` em bytes: {}", std::mem::size_of_val(&y));
    println!("tamanho de `z` em bytes: {}", std::mem::size_of_val(&z));
    println!("tamanho de `i` em bytes: {}", std::mem::size_of_val(&i));
    println!("tamanho de `f` em bytes: {}", std::mem::size_of_val(&f));
}
```

Alguns conceitos usados no código acima ainda nao foram explicados,
segue uma breve explicacao para os leitores impacientes:

* `fun(&foo)` é usado para passar um argumento à uma funcao *por referência*, invés
  de por valor (`fun(foo)`). Para mais detalhes sobre [emprestimo][borrow].
* `std::mem::size_of_val` é uma funcao, mas chamado com seu *caminho completo*. Código
  pode ser dividido em unidade lógicas chamadas *modulos*. Nesse caso,
  a funcao `size_of_val` é definidia no módulo `mem`, e o módulo `mem`
  é definido no *crate* `std`. Para mais detalhes, veja
  [modulos][mod] e [crates][crate].

[borrow]: ../scope/borrow.md
[mod]: ../mod.md
[crate]: ../crates.md
