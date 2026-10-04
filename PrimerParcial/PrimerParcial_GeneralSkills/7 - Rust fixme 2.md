### Descripción
The Rust saga continues? I ask you, can I borrow that, pleeeeeaaaasseeeee?

Download the Rust code [here](https://challenge-files.cylabacademy.net/library/048c73621a97b98cde18eae5a9495279f2396cb64c65235bb310e7ad26d726ac/fixme2.tar.gz).

Hint: [https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html)
### Solución

1. Descargamos el archivo y lo extraemos:

```
~/cylab via 🐍 v3.13.5 
❯ wget https://challenge-files.cylabacademy.net/library/048c73621a97b98cde18eae5a9495279f2396cb64c65235bb310e7ad26d726ac/fixme2.tar.gz

~/cylab via 🐍 v3.13.5 took 2s 
➜ tar -xzf fixme2.tar.gz
```

2. Navegamos a fixme2/src y veremos el archivo main.rs:
```
~/cylab/fixme2 via 🦀 v1.94.1 
➜ ls
Cargo.lock  Cargo.toml  src

~/cylab/fixme2 via 🦀 v1.94.1 
➜ cd src

cylab/fixme2/src via 🦀 v1.94.1 
➜ ls
main.rs
```

3. Entramos con nano al archivo y corregimos los errores de mutabilidad guiándonos por los comentarios y errores del compilador. El primer cambio es decirle a la función que recibirá una referencia mutable (`&mut String`), el segundo es declarar la variable `party_foul` como mutable con `mut`, y el tercero es enviar la variable a la función con el prefijo `&mut`:

```
use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer:Vec<u8>, borrowed_string: &mut String){ // How do we pass values to a function that we want to change?
    // Key for decryption
    let key = String::from("CSUCKS");

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return; 
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");
    borrowed_string.push_str(&String::from_utf8_lossy(&decrypted_buffer));
    println!("{}", borrowed_string);
}


fn main() {
    // Encrypted flag values
    let hex_values = ["71", "35", "11", "73", "2f", "17", "53", "71", "01", "1c", "7e", "59", "63", "e1", "61", "25", "0d"]; // (Truncado por legibilidad)

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let mut party_foul = String::from("Using memory unsafe languages is a: "); // Is this variable changeable?
    decrypt(encrypted_buffer, &mut party_foul); // Is this the correct way to pass a value to a function so that it can be changed?
}
```

4. Regresamos a la carpeta de fixme2 y ejecutamos el proyecto con el comando 'cargo run' para que nos de la flag:

```
~/cylab/fixme2/src via 🦀 v1.94.1 took 30s 
➜ cd ..

~/cylab/fixme2 via 🦀 v1.94.1 
➜ cargo run
   Compiling rust_proj v0.1.0 (/home/rubi/cylab/fixme2)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.90s
     Running `target/debug/rust_proj`
Using memory unsafe languages is a: PARTY FOUL! Here is your flag: academy{4r3_y0u_h4v1n5_fun_y31?}
```

**Flag**: academy{4r3_y0u_h4v1n5_fun_y31?}

### Notas Adicionales

En Rust, las variables y las referencias son inmutables por defecto. Para modificar una variable dentro de una función, es necesario declarar tanto la variable original, como la referencia que se pasa, y el parámetro que la recibe, utilizando la palabra clave `mut`.

### Referencias

- [Rust Book: Variables and Mutability](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html)
    
- [Rust Book: References and Borrowing](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html)