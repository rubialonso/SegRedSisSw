### Descripción
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!
Download the Rust code [here](https://challenge-files.cylabacademy.net/library/b9cfc84c442958b8ac848ddc0692bed9ef01a15877b8d37f36afbe68b5849acc/fixme1.tar.gz)

Hints
1. Cargo is Rust's package manager and will make your life easier. See the getting started page [here](https://doc.rust-lang.org/book/ch01-03-hello-cargo.html)
2. [println!](https://doc.rust-lang.org/std/macro.println.html)
3. Rust has some pretty great compiler error messages. Read them maybe?
### Solución
1. Descargamos el archivo y lo extraemos: 
```
~/cylab via 🐍 v3.13.5 took 2s 
➜ wget https://challenge-files.cylabacademy.net/library/b9cfc84c442958b8ac848ddc0692bed9ef01a15877b8d37f36afbe68b5849acc/fixme1.tar.gz

~/cylab via 🐍 v3.13.5 took 2s 
➜ tar -xzf fixme1.tar.gz
```

2. Navegamos a fixme1/src veremos el archivo main.rs: 
```
~/cylab/fixme1 via 🦀 v1.94.1 
➜ ls
Cargo.lock  Cargo.toml  src

~/cylab/fixme1 via 🦀 v1.94.1 
➜ cd src

cylab/fixme1/src via 🦀 v1.94.1 
➜ ls
main.rs
```

3. Entramos con nano al archivo y corregimos los 3 errores de sintaxis guiandonos por los comentarios. El primero el colocar el ';' al final de la línea, el segundo es completar la línea para que diga return; y el tercero es colocar las llaves {} faltantes para que quede como "{:?}" : 
```
	use xor_cryptor::XORCryptor;

fn main() {
    // Key for decryption
    let key = String::from("CSUCKS"); // How do we end statements in Rust?

    // Encrypted flag values
    let hex_values = ["71", "35", "11", "73", "2f", "17", "53", "71", "01", "1c", "7e", "59", "63", "e1", "61", "25", "7f", "5a", "60", "50", "11", "38", "1f", "3a", "60", "e9", "62", "20", "0c", "e6", "50", "d3", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    println!(
        "{:?}", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```

4. Regresamos a la carpeta de fixme1 y ejecutamos el archivo cargo.toml con el comando 'cargo run' para que nos de la flag: 
```
	cylab/fixme1/src via 🦀 v1.94.1 took 1m7s 
➜ cd ..

~/cylab/fixme1 via 🦀 v1.94.1 
➜ cargo run
    Updating crates.io index
  Downloaded xor_cryptor v1.2.3
  Downloaded crossbeam-deque v0.8.5
  Downloaded crossbeam-utils v0.8.20
  Downloaded crossbeam-epoch v0.9.18
  Downloaded either v1.13.0
  Downloaded rayon-core v1.12.1
  Downloaded rayon v1.10.0
  Downloaded 7 crates (379.2KiB) in 2.05s
   Compiling crossbeam-utils v0.8.20
   Compiling rayon-core v1.12.1
   Compiling either v1.13.0
   Compiling crossbeam-epoch v0.9.18
   Compiling crossbeam-deque v0.8.5
   Compiling rayon v1.10.0
   Compiling xor_cryptor v1.2.3
   Compiling rust_proj v0.1.0 (/home/rubi/cylab/fixme1)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 16.16s
     Running `target/debug/rust_proj`
"academy{4r3_y0u_4_ru$t4c30n_n0w?}"
```

**Flag**: academy{4r3_y0u_4_ru$t4c30n_n0w?}
### Notas Adicionales

### Referencias