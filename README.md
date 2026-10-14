# face

Digitalt robotansikte (HRI-01) för forskning inom människa–robot-interaktion. Ansiktet visar känslor och reagerar på användaren, så att det kan simulera en robot i försök.

**Demo:** https://peterparnes.github.io/face/

## Köra

Allt ligger i en enda fil, `index.html`. Öppna den i en webbläsare. Ingen server och inget byggsteg behövs. Utan internet används systemets typsnitt i stället för IBM Plex.

## Funktioner

- **Känslor:** tio förinställningar med FACS-referenser (tangent 0–9). Intensiteten och övergångstiden går att ställa in.
- **Ansiktsparametrar:** 17 reglage för ögonbryn, ögonlock, pupiller, mun, huvud och blick. Inställningen kan kopieras som JSON.
- **Beteende:** automatisk blinkning, blick som följer pekaren och små rörelser i viloläge.
- **Interaktion:** ett klick på ansiktet ger en skrämselreaktion. Inskriven text animerar munnen, med valfri talsyntes.
- **Händelselogg:** alla händelser loggas med tidsstämpel i millisekunder och kan exporteras som JSON.
- **Försöksläge:** **H** döljer panelen och **F** ger helskärm.

## Styrning från kod

```js
face.setEmotion('joy', 0.8, 400)  // känsla, intensitet 0–1, övergång i ms
face.lookAt(0.4, -0.2, 2)         // x, y i [-1, 1], hålltid i sekunder
face.blink()
face.say('Hej på dig')
face.setParam('smile', 0.5)
face.getState()
face.getLog()
```

När sidan är inbäddad i en iframe:

```js
iframe.contentWindow.postMessage({ type: 'face', cmd: 'setEmotion', args: ['anger', 0.6], id: 1 }, '*')
// svar: { type: 'face:result', id: 1, result: ... }
```

Varje loggad händelse skickas också som `face:event` (CustomEvent) på `window`.

Känslor: `neutral`, `joy`, `sadness`, `anger`, `fear`, `surprise`, `disgust`, `contempt`, `thinking`, `sleepy`.
