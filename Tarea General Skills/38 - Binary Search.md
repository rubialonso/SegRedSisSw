### Descripción
Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses.

Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools!

Hints:
- Have you ever played hot or cold? Binary search is a bit like that.
- You have a very limited number of guesses. Try larger jumps between numbers!
- The program will randomly choose a new number each time you connect. You can always try again, but you should start your binary search over from the beginning - try around 500. Can you think of why?
### Solución
Se descargo el archivo, se descomprimio y revise que habia. De ahi abri el servidor y empece a adivinar partiendo por mitad cada numero que ponia primero por mitad 500, la mitad de 500 → 250 y asi hasta llegar a 8, pero pues era más grande y el 10 lo puse nomás por ocurrencia no pense mucho
```
~/cylab via 🐍 v3.13.5 
➜ wget https://artifacts.picoctf.net/c_atlas/6/challenge.zip

~/cylab via 🐍 v3.13.5 took 2s 
➜ unzip challenge.zip 

home/ctf-player/drop-in 
➜ ls
guessing_game.sh

home/ctf-player/drop-in 
❯ ssh -p 62749 ctf-player@atlas.picoctf.net

Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Lower! Try again.
Enter your guess: 250
Lower! Try again.
Enter your guess: 125
Lower! Try again.
Enter your guess: 63
Lower! Try again.
Enter your guess: 31
Lower! Try again.
Enter your guess: 15
Lower! Try again.
Enter your guess: 8
Higher! Try again.
Enter your guess: 10
Congratulations! You guessed the correct number: 10
Here's your flag: picoCTF{g00d_gu355_de9570b0}
Connection to atlas.picoctf.net closed.
```
**Flag**: picoCTF{g00d_gu355_de9570b0}
### Notas Adicionales
La búsqueda binaria es un algoritmo eficiente para encontrar un elemento de una lista ordenada de elementos. Funciona dividiendo repetidamente por la mitad la parte de la lista que podría contener el elemento, hasta que hayas reducido las posibles ubicaciones a solo una.
### Referencias
https://www.khanacademy.org/computing/computer-science/algorithms/binary-search/a/binary-search