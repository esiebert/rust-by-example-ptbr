# Literais e operadores

Inteiros `1`, floats `1.2`, caracteres `'a'`, strings `"abc"`, booleanos `true`
e o tipo de unidade `()` podem ser expressados usando literais.

Inteiros podem também se expressados usando notacao hexadecimal, octal ou binária
usando os respectivos prefixos: `0x`, `0o` ou `0b`.

Underscore pode ser usado em literais numéricos para melhorar a legibilidade, e.g.
`1_000` é o mesmo que `1000`, e `0.000_001` é o mesmo que `0.000001`.

Nós precisamos indicar ao compilador o tipo de literais que queremos usar. Por ora,
usaremos o sufixo `u32` para indicar que um literal é inteiro de 32 bits nao-assinado
, e o sufixo `i32` para indicar que é um inteiro de 32 bits assinado.

Os operadores disponíveis e sua precedência [em Rust][rust op-prec] sao iguais a outras
linguagens [similares a C][op-prec].

```rust,editable
fn main() {
    // Adicao de inteiros
    println!("1 + 2 = {}", 1u32 + 2);

    // Subtracao de inteiros
    println!("1 - 2 = {}", 1i32 - 2);
    // TODO ^ Troque `1i32` para `1u32` para ver porque o tipo é importante

    // Curto circuito de lógica booleana
    println!("true AND false é {}", true && false);
    println!("true OR false é {}", true || false);
    println!("NOT true é {}", !true);

    // Operacoes em bits
    println!("0011 AND 0101 é {:04b}", 0b0011u32 & 0b0101);
    println!("0011 OR 0101 é {:04b}", 0b0011u32 | 0b0101);
    println!("0011 XOR 0101 é {:04b}", 0b0011u32 ^ 0b0101);
    println!("1 << 5 é {}", 1u32 << 5);
    println!("0x80 >> 2 é 0x{:x}", 0x80u32 >> 2);

    // Usando underscores para melhorar legibilidade!
    println!("Um milhao é escrito como {}", 1_000_000u32);
}
```

[rust op-prec]: https://doc.rust-lang.org/reference/expressions.html#expression-precedence
[op-prec]: https://en.wikipedia.org/wiki/Operator_precedence#Programming_languages
