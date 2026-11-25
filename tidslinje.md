# Tidslinje: rita vad som händer

Välj snutt 5 och snutt 10. Fyll i tabellerna steg för steg. Skriv vad som ligger i varje del **efter** varje steg.

Förklaring:

- **Anropsstacken** är den kod som körs just nu.
- **Microtask-kön** är promise-callbacks som väntar på att få köra.
- **Task-kön** är timer-callbacks och liknande som väntar på att få köra.
- Regel: när stacken är tom körs först ALLA microtasks, sedan EN task, sedan tomma microtasks igen, och så vidare.

## Snutt 5

| Steg | Vad händer                          | Stacken | Microtask-kön | Task-kön | Utskrift hittills      |
| ---- | ----------------------------------- | ------- | ------------- | -------- | ---------------------- |
| 1    | setTimeout anropas                  | script  | –             | timeout  | –                      |
| 2    | Promise.resolve().then(...) anropas | script  | promise       | timeout  | –                      |
| 3    | console.log("sync")                 | script  | promise       | timeout  | sync                   |
| 4    | Stacken tom: vad körs först?        | –       | –             | timeout  | sync, promise          |
| 5    | Nästa                               | –       | –             | –        | sync, promise, timeout |

## Snutt 10

| Steg | Vad händer                       | Stacken | Microtask-kön | Task-kön     | Utskrift hittills |
| ---- | -------------------------------- | ------- | ------------- | ------------ | ----------------- |
| 1    | console.log("1")                 | script  | –             | –            | 1                 |
| 2    | första setTimeout                | script  | –             | timeout 2    | 1                 |
| 3    | Promise.resolve().then(3)        | script  | promise 3     | timeout 2    | 1                 |
| 4    | andra setTimeout                 | script  | promise 3     | timeout 2, 4 | 1                 |
| 5    | console.log("6")                 | script  | promise 3     | timeout 2, 4 | 1, 6              |
| 6    | stacken tom, microtask-kön först | –       | –             | timeout 2, 4 | 1, 6, 3           |
| 7    | första tasken                    | –       | –             | timeout 4    | 1, 6, 3, 2        |
| 8    | andra tasken                     | –       | promise 5     | –            | 1, 6, 3, 2, 4     |
| 9    | microtask 5                      | –       | –             | –            | 1, 6, 3, 2, 4, 5  |

## Min förklaring i en mening

Varför kommer en promise-callback före en timer med 0 ms?

A promise callback runs before a timer with 0 ms, because microtasks are executed before the next task when the call stack is empty.
