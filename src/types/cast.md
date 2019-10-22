# Conversao (Casting)

Rust nao fornece conversao implicita de tipos (coercao) entre tipos primitivos.
Porém, conversao explicita (casting) pode ser feita usando a palavra-chave `as`.

Regras para conversao entre tipos integrais seguem convencoes C,
exceto em casos onde C tem comportamento indefinido. O comportamento de conversoes
entre tipos integrais é bem definidio em Rust.

```rust,editable,ignore,mdbook-runnable
// Silenciar alertas de conversao que causam overflow.
#![allow(overflowing_literals)]

fn main() {
    let decimal = 65.4321_f32;

    // Erro! Conversao nao implicita
    let inteiro: u8 = decimal;
    // FIXME ^ Comente essa linha

    // Conversao explicita
    let inteiro = decimal as u8;
    let character = inteiro as char;

    println!("Conversao: {} -> {} -> {}", decimal, inteiro, character);

    // conversoes de qualquer valor para um tipo nao assinado (T) ocorrem,
    // std::T::MAX + 1 é adicionado ou subtraído até que o valor caiba no
    // novo tipo

    // 1000 já cabe em u16
    println!("1000 como um u16 é: {}", 1000 as u16);

    // 1000 - 256 - 256 - 256 = 232
    // Debaixo do capô, os 8 menos significantes bits (LSB) sao mantido,
    // enquanto o resto dos mais significantes (MSB) sao truncados.
    println!("1000 como um u8 é : {}", 1000 as u8);
    // -1 + 256 = 255
    println!("  -1 como um u8 é : {}", (-1i8) as u8);

    // Para números positivos, é a mesma coisa que um módulo
    println!("1000 mod 256 é : {}", 1000 % 256);

    // Quando convertido para um tipo assinado, o resultado bit por bit é o mesmo que
    // converter para o tipo nao assinado. Se o bit mais significante for 1, 
    // entao o valor é negativo.

    // Exceto no caso que este valor já caiba no novo tipo.
    println!(" 128 como um i16 é: {}", 128 as i16);
    // 128 como u8 -> 128, cujo complemento de 2 em oito bits é:
    println!(" 128 como um i8 é : {}", 128 as i8);

    // repetindo o exemplo acima
    // 1000 como u8 -> 232
    println!("1000 como um u8 é : {}", 1000 as u8);
    // e o complemento de dois de 232 é -24
    println!(" 232 como um i8 é : {}", 232 as i8);
}
```
