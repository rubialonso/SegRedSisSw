### Descripción

The name of the game is speed. Are you quick enough to solve this problem and keep it above 50 mph? need-for-speed

Hint: What is the final key?

### Solución

1. Descargar el binario `need-for-speed` y darle permisos de ejecución. No está "stripped", así que se conservan los nombres de las funciones (`set_timer`, `get_key`, `calculate_key`, `decrypt_flag`, `print_flag`, `alarm_handler`, etc.).
2. Al correr el binario directamente, falla casi de inmediato:

```
$ time ./nfs
Keep this thing over 50 mph!
=============================

Creating key...
Not fast enough. BOOM!

real    0m1.066s
```

3. Analizando `set_timer` con `objdump -d -M intel` se ve que registra un manejador de señal para `SIGALRM` (`signal(14, alarm_handler)`) y llama a `alarm(1)`, es decir, da sólo **1 segundo** antes de "explotar".
4. Analizando `calculate_key` se ve que es un bucle "quema-tiempo": parte de un valor fijo `0xcf5e0af6`, lo decrementa en un bucle hasta llegar a otro valor fijo `0xe7af057b`, y repite esto 8 veces. El resultado final siempre es el mismo valor constante `0xe7af057b` (no depende de nada externo ni de tiempo real), pero tarda bastante más de 1 segundo en ejecutarse completo, por lo que la alarma siempre se dispara antes de terminar en ejecución normal.
5. La solución es usar `gdb` para saltarse ese bucle: ponemos un breakpoint justo antes de que `get_key` llame a `calculate_key`, y en cuanto se detiene ahí, ponemos manualmente `eax = 0xe7af057b` (el resultado que ese bucle siempre produce) y movemos `$rip` para saltarnos la llamada por completo, evitando así el tiempo de cómputo y la alarma:

```
$ gdb -q -batch \
    -ex 'break *get_key+0x1c' \
    -ex 'run' \
    -ex 'set $eax = 0xe7af057b' \
    -ex 'set $rip = get_key+0x21' \
    -ex 'continue' \
    ./nfs

Breakpoint 1, 0x0000566ad50e6338 in get_key ()
Keep this thing over 50 mph!
=============================

Creating key...
Finished
Printing flag:
academy{Good job keeping bus #31326f14 speeding along!}
[Inferior 1 (process 379) exited normally]
```

**Flag**: academy{Good job keeping bus #31326f14 speeding along!}

### Notas Adicionales

El "truco" del reto no es escribir código ni jugar el juego de velocidad en sí, sino notar que `calculate_key` siempre produce el mismo valor constante (sólo simula tardanza), y que la única forma realista de superarlo a tiempo es manipular la ejecución con el depurador para obtener ese valor sin esperar a que el bucle termine.

### Referencias