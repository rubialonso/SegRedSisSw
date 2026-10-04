### Descripción
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!

Hint: Read the comments...darn it! 
### Solución
1. Descargamos el archivo comprimido `fixme3.tar.gz` y lo extraemos:
```
~/cylab via 🐍 v3.13.5 took 2s 
➜ wget https://challenge-files.cylabacademy.net/library/6df8b7779faf29e53f515922041d99bc26381a332ca090c291ba20577ac7cf92/fixme3.tar.gz

~/cylab via 🐍 v3.13.5 took 2s 
➜ tar -xzf fixme3.tar.gz
```

2. Navegamos a `fixme3/src` y veremos el archivo `main.rs`:
```
~/cylab/fixme3 via 🦀 v1.94.1 
➜ ls
Cargo.lock  Cargo.toml  src

~/cylab/fixme3 via 🦀 v1.94.1 
➜ cd src

cylab/fixme3/src via 🦀 v1.94.1 
➜ ls
main.rs
```

3. Entramos con nano al archivo y corregimos los errores de sintaxis guiándonos por los comentarios, tal como lo indica la pista. El problema de este tercer reto radica en el uso de punteros crudos ("raw pointers"). En Rust, llamar a una función que manipula la memoria a través de punteros (como `std::slice::from_raw_parts`) es considerado inseguro por el compilador, por lo que exige que esa porción de código esté explícitamente envuelta en un bloque `unsafe { }`. Corregimos la línea problemática añadiendo la declaración de seguridad:
```
    use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer:Vec<u8>, borrowed_string: &mut String){ 
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
    
    let decrypted_ptr = decrypted_buffer.as_ptr();
    let decrypted_len = decrypted_buffer.len();

    // UNSAFE: Dereferencing a raw pointer must be wrapped in an unsafe block.
    let decrypted_slice = unsafe { std::slice::from_raw_parts(decrypted_ptr, decrypted_len) };

    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");
    borrowed_string.push_str(&String::from_utf8_lossy(decrypted_slice));
    println!("{}", borrowed_string);
}

fn main() {
    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "12", "90", "7e", "53", "63", "e1", "01", "35"]; // (Truncado por legibilidad)

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let mut party_foul = String::from("Using memory unsafe languages is a: "); 
    decrypt(encrypted_buffer, &mut party_foul); 
}
```

4. Regresamos a la carpeta de fixme3 y ejecutamos el proyecto con el comando `cargo run` para que nos entregue la bandera:
```
cylab/fixme3/src via 🦀 v1.94.1 took 30s 
➜ cd ..

~/cylab/fixme3 via 🦀 v1.94.1 
➜ cargo run
```

**Flag**: academy{n0w_y0uv3_f1x3d_1h3m_411}
### Notas Adicionales

En Rust, el código que lee o modifica la memoria directamente mediante punteros crudos se considera inseguro porque el compilador pierde su capacidad de garantizar automáticamente las reglas estrictas de propiedad (ownership) y préstamo (borrowing). Al implementar un bloque `unsafe { }`, el desarrollador asume la responsabilidad de que la operación es válida y no causará desbordamientos de búfer o lecturas no autorizadas.
### Referencias