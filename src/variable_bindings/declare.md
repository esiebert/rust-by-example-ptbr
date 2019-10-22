# Declaracao por primeiro

É possível declarar vinculos de variável por primeiro e inicializa-los depois.
Porém essa forma é raramente utilizada, visto que pode levar a variáveis nao inicializadas.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Declara um vínculo
    let um_vinculo;

    {
        let x = 2;

        // Inicializa o vínculo
        a_binding = x * x;
    }

    println!("um vínculo: {}", um_vinculo);

    let outro_vinculo;

    // Erro! Uso the vínculo nao inicializado
    println!("outro vínculo: {}", outro_vinculo);
    // FIXME ^ Comente essa linha

    outro_vinculo = 1;

    println!("outro vínculo: {}", outro_vinculo);
}
```

O compilador proíbe o uso de variáveis nao inicializadas visto que isso pode levar
a comportamento indefinido.
