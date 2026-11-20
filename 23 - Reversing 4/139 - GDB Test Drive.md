### Descripción

Can you get the flag? Download this binary.

Here's the test drive instructions:

- `$ chmod +x gdbme`
- `$ gdb gdbme`
- `(gdb) layout asm`
- `(gdb) break *(main+99)`
- `(gdb) run`
- `(gdb) jump *(main+104)`

### Solución

1. Descargar el binario `gdbme` desde el enlace del reto y darle permisos de ejecución (`chmod +x gdbme`).
2. Seguir exactamente las instrucciones que da el propio enunciado: abrir el binario con `gdb`, poner un breakpoint en `*(main+99)`, correrlo, y una vez detenido en ese breakpoint hacer un `jump` directo a `*(main+104)`, saltándose así las instrucciones intermedias (que son las que normalmente provocarían que el programa fallara/terminara sin mostrar la flag).
3. En el servidor ejecutamos esto en modo batch para automatizar los mismos pasos:

```
$ gdb -q -batch -ex 'break *(main+99)' -ex 'run' -ex 'jump *(main+104)' ./gdbme
Breakpoint 1 at 0x132a
warning: Error disabling address space randomization: Operation not permitted
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x0000565d25fa832a in main ()
academy{d3bugg3r_dr1v3_4cc75120}
[Inferior 1 (process 322) exited normally]
```

**Flag**: academy{d3bugg3r_dr1v3_4cc75120}

### Notas Adicionales

El `jump` dentro de `gdb` permite saltarse manualmente las instrucciones de máquina ubicadas entre `main+99` y `main+104` (probablemente una comparación/condición que normalmente evita que se imprima la flag), forzando al programa a ejecutar directamente el código que sí la imprime.

### Referencias