### Descripción

Now you DON'T see me. This report has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly? [Financial_Report_for_ABC_Labs.pdf](https://challenge-files.cylabacademy.net/library/455e6e9581a9272cf0cd6a8f2da0a7cdcfefdb52dc7a7f9c09a27705e2c94103/Financial_Report_for_ABC_Labs.pdf)

### Solución

1. Descargar el PDF.
2. El documento visualmente muestra partes "tapadas" (redactadas) con rectángulos negros, pero esos rectángulos son solo un objeto gráfico superpuesto al texto — el texto real sigue estando en el stream del PDF.
3. En vez de abrir el PDF visualmente, se extrae el texto crudo con `pdftotext`:

```bash
   pdftotext -layout Financial_Report_for_ABC_Labs.pdf -
```

4. La salida revela el texto que debería estar oculto, incluida la flag:

```
   Financial Report for ABC Labs, Kigali, Rwanda for the year 2021.
   Breakdown - Just painted over in MS word.
   ...
   This is not the flag, keep looking
   Expenses from the
   academy{C4n_Y0u_S33_m3_fully}
   Redacted document.
```

**Flag:** `academy{C4n_Y0u_S33_m3_fully}`

### Notas Adicionales

El reto incluye un señuelo explícito ("This is not the flag, keep looking") para que no se confunda con un texto parecido a flag que aparece antes. La lección de fondo: "redactar" pintando un rectángulo encima del texto (como en MS Word) no borra el texto subyacente del documento.

### Referencias