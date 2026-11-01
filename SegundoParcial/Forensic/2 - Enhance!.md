### Descripción
Download this image file and find the flag.

- [Download image file](https://challenge-files.cylabacademy.net/library/83bfcd323363337f297f4d4ee3bff06df8564155aa2037148151710fa8baec04/drawing.flag.svg)
### Solución
1. Descargar el archivo con wget
2. Usamos el comando tail:
```
~/cylab/sp_forensic 
➜ tail -n 20 drawing.flag.svg
         y="132.10265"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3760">e </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10706"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3762">m </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11147"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3764">y { 3 n h 4 n </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11588"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3752">c 3 d _ 5 b 5 e 6 f 1 8 }</tspan></text>
  </g>
</svg>
```

3. Al final se mira la flag dividida en 2 y con espacios entre los tspan: { 3 n h 4 nc 3 d _ 5 b 5 e 6 f 1 8 }
**Flag**: academy{3nh4nc3d_5b5e6f18}
### Notas Adicionales

### Referencias