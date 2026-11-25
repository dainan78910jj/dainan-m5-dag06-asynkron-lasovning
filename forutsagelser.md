# Förutsägelser: asynkron kod

Regler:

1. Titta på snutten i `snuttar/sNN.js` (eller på sidan `index.html`). **Kör den inte än.**
2. Skriv din gissning i tabellen: utskrifterna i den ordning du tror att de kommer, separerade med `|`.
3. Kör snutten (knappen _Kör_). Skriv vad som faktiskt skrevs ut.
4. Hade du rätt? Skriv en regel med egna ord för varje snutt du gissade fel på.

| Snutt | Min gissning (i ordning)                         | Faktisk utskrift                                 | Rätt? | Min regel om jag hade fel                                          |
| ----- | ------------------------------------------------ | ------------------------------------------------ | ----- | ------------------------------------------------------------------ |
| 1     | 1,2,3                                            | 1,2,3                                            | Yes   |                                                                    |
| 2     | A,B,C                                            | A,C,B                                            | No    | setTimeout takes time to init                                      |
| 3     | start, noll, kort, lång                          | start, noll, kort, lång                          | Yes   |                                                                    |
| 4     | efter, inuti promise, then:klart                 | inuti promise, efter, then:klart                 | No    | promise starts right after while then starts after the main thread |
| 5     | sync, timeout, promise                           | sync, promise, timeout                           | No    | promise has higher priority then timeout                           |
| 6     | först?, 6, 7                                     | först?, 6, 7                                     | Yes   |                                                                    |
| 7     | fel: slut på mjölk, städar                       | fel: slut på mjölk, städar                       | Yes   |                                                                    |
| 8     | beställer, sätter mig, bullen klar, kaffet klart | beställer, sätter mig, bullen klar, kaffet klart | Yes   |                                                                    |
| 9     | väntar på båda, ['kaffe', 'bulle']               | väntar på båda, ['kaffe', 'bulle']               | Yes   |                                                                    |
| 10    | 1,6,3,2,4,5                                      | 1,6,3,2,4,5                                      | Yes   |                                                                    |
| 11    | c, ab                                            | c, ab                                            | Yes   |                                                                    |

## Tre meningar med egna ord

1. JavaScript does not wait for `setTimeout`; instead, it schedule the timeout callback to another task.
2. A promise has three states: pending, resolved, rejected.
3. `then` is always executed after promise is resolved.
