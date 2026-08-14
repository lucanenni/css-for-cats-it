<span class="bigTitle">CSS per Gatti</span>
## Un'introduzione gentile allo stile per programmatori alle prime armi <span class="right">![cat](images/yarn.svg)</span>
### *Perché una pagina in Times New Roman su sfondo bianco non è vita*

CSS sta per **Cascading Style Sheets**, fogli di stile a cascata. Se l'HTML è lo scheletro di una pagina (vai a leggere prima [HTML per Gatti](https://github.com/lucanenni/html-for-cats-it) se non l'hai ancora fatto), il CSS è il pelo, il colore, l'atmosfera generale. È quello che prende un semplice elenco di titoli e paragrafi e lo trasforma in qualcosa di effettivamente progettato invece che in un documento legale. Colori, font, spaziature, layout, persino piccole animazioni &mdash; tutto CSS.

Ogni browser capisce il CSS così come capisce l'HTML, il che significa che puoi prendere una pagina e darle una personalità completamente diversa semplicemente cambiando quale CSS le è collegato &mdash; stesso scheletro, pelo diverso. Questa pagina ti insegnerà abbastanza CSS da smettere di averne paura*.

\* *Tempo reale: più di zero. Passerai sicuramente quindici di quei minuti a cercare di ottenere esattamente la giusta sfumatura di arancione. È normale, lo fanno tutti.*

CSS per Gatti è distribuito con licenza [CC0](https://creativecommons.org/publicdomain/zero/1.0/deed.it) &mdash; fanne quello che vuoi.

*Questo è un tutorial originale non ufficiale, scritto nello stile di [JavaScript for Cats](https://github.com/max-mapper/javascript-for-cats) di [@maxogden](http://twitter.com/maxogden), e compagno di [HTML per Gatti](https://github.com/lucanenni/html-for-cats-it). Non è una traduzione, non è ufficiale &mdash; solo altro omaggio.*

## Indice

- [Non fare il gatto pauroso](#scaredy-cat)
- [Collegare gli stili a una pagina](#attaching)
- [Selettori](#selectors)
- [Proprietà e valori](#properties)
- [Classi e ID](#classes-ids)
- [La cascata](#cascade)
- [Colori](#colors)
- [Il box model](#box-model)
- [Testo e font](#text)
- [Display](#display)
- [Flexbox, in breve](#flexbox)
- [Pseudo-classi](#pseudo-classes)
- [Design responsive](#responsive)
- [Letture consigliate](#recommended-reading)

## <a id="scaredy-cat" href="#scaredy-cat">#</a> Non fare il gatto pauroso

Stesso discorso di sempre: niente di quello che fai qui può rompere niente in modo permanente. Nel peggiore dei casi una scatola diventa di un brutto verde, o il tuo testo finisce di traverso, o tutto si accatasta in un mucchio come un cestino di gattini. Ricarichi la pagina e sparisce tutto. Gli errori di CSS sono gli errori più sicuri di tutta la programmazione &mdash; abbracciali, è così che impari dove sono davvero i bordi della scatola.

## <a id="attaching" href="#attaching">#</a> Collegare gli stili a una pagina

Ci sono tre modi per collegare il CSS all'HTML, e li incontrerai tutti e tre in giro, anche se uno è chiaramente il migliore per qualsiasi cosa oltre un rapido esperimento.

**Inline**, direttamente su un elemento, usando l'attributo `style`. Veloce, ma disordinato, e influenza solo quell'elemento:

```html
<p style="color: orange;">Questo paragrafo è arancione, e solo questo.</p>
```

**Interno**, in un tag `<style>` dentro l'`<head>` della tua pagina. Influenza l'intera pagina, senza bisogno di un file separato:

```html
<head>
  <style>
    p {
      color: orange;
    }
  </style>
</head>
```

**Esterno**, in un file `.css` separato, collegato dall'`<head>` con un tag `<link>`. È quello che vuoi per qualsiasi cosa reale, perché mantiene lo stile separato dalla struttura, e un unico foglio di stile può dare lo stile a *molte* pagine contemporaneamente:

```html
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

```css
/* style.css */
p {
  color: orange;
}
```

Da qui in poi, dai per scontato che tutto viva in un foglio di stile esterno.

## <a id="selectors" href="#selectors">#</a> Selettori

Una regola CSS ha due parti: un **selettore**, che dice *a quali elementi* si applica questa regola, e un blocco di **dichiarazioni** tra parentesi graffe, che dice *cosa fare* a quegli elementi. Il selettore più semplice è solo il nome di un tag:

```css
p {
  color: orange;
}
```

Questo dice: "ogni `<p>` sulla pagina, rendi il testo arancione". Tutto qui. È l'intera idea del CSS, ripetuta all'infinito con selettori più elaborati e dichiarazioni più elaborate: *seleziona qualcosa, poi descrivilo.*

## <a id="properties" href="#properties">#</a> Proprietà e valori

Dentro le parentesi graffe, ogni riga è una **proprietà** (quale aspetto stai cambiando) seguita da due punti, poi un **valore** (a cosa lo stai cambiando), e termina con un punto e virgola:

```css
p {
  color: orange;
  font-size: 20px;
  text-align: center;
}
```

Esistono centinaia di proprietà. Non le memorizzerai tutte, e non serve &mdash; nemmeno i gatti professionisti le sanno tutte a memoria. Ti costruirai un piccolo vocabolario di lavoro (`color`, `font-size`, `margin`, `padding`, `background`...) e cercherai il resto quando ti servirà, un po' come conosci il suono di un solo sacchetto di premietti specifico in mezzo a tutta una dispensa di alimentari.

## <a id="classes-ids" href="#classes-ids">#</a> Classi e ID

Selezionare *ogni* `<p>` di una pagina spesso è troppo generico. Per puntare a qualcosa di più specifico, gli elementi HTML possono avere un attributo `class` o `id`, e il CSS può selezionare in base a quelli invece che al nome del tag.

```html
<p class="avviso">Non avvicinarti al cetriolo.</p>
<p id="titolo-principale">Gatto Locale Scopre Un Raggio Di Sole</p>
```

```css
.avviso {
  color: red;
  font-weight: bold;
}

#titolo-principale {
  font-size: 32px;
}
```

Nota la punteggiatura: un `.` davanti per le classi, un `#` davanti per gli ID. La differenza tra i due: una **classe** può essere riutilizzata su tutti gli elementi che vuoi (perfetta per "ogni elemento che ha bisogno di questo trattamento particolare"), mentre un **id** dovrebbe comparire esattamente una volta per pagina (è un nome unico per un elemento specifico, come un microchip).

```html
<p class="avviso">Non avvicinarti al cetriolo.</p>
<p class="avviso">Sul serio. Non farlo.</p>
```

Entrambi i paragrafi sopra ricevono lo stile `.avviso`, perché le classi sono pensate per essere condivise.

## <a id="cascade" href="#cascade">#</a> La cascata

La "C" di CSS sta per **Cascading**, un modo elegante per descrivere cosa succede quando più di una regola cerca di dare stile allo stesso elemento. Le regole più in basso in un foglio di stile generalmente vincono su quelle più in alto, *ma* i selettori più specifici generalmente vincono su quelli meno specifici, indipendentemente dall'ordine. Un ID batte una classe, una classe batte il nome di un tag:

```css
p { color: black; }
.avviso { color: red; }
#titolo-principale { color: blue; }
```

Un paragrafo con `class="avviso"` diventa rosso, non nero, anche se si applica anche `p { color: black; }` &mdash; la classe è più specifica, quindi vince. È un po' come una casa con un programma dei pasti del gatto attaccato al frigo (la regola sul tag, "tutti mangiano lo stesso cibo") e un biglietto del veterinario attaccato sopra in penna rossa (la regola sulla classe o sull'id, "*questo* gatto qui ha bisogno del cibo speciale") &mdash; l'istruzione più specifica vince, e tutti in qualche modo lo sanno, senza che nessuno lo abbia mai spiegato del tutto.

Questa è, sinceramente, la parte del CSS che manda più in confusione. Quando uno stile "non funziona", il 90% delle volte è perché qualcosa di *più specifico* altrove lo sta silenziosamente scavalcando. Apri l'Ispettore (lo stesso di HTML per Gatti) e clicca sull'elemento &mdash; ti mostrerà esattamente quali regole sono in competizione e quale ha vinto.

## <a id="colors" href="#colors">#</a> Colori

I colori in CSS si presentano in alcuni formati diversi, e li vedrai tutti:

```css
p {
  color: orange;               /* un colore con nome */
  color: #ffa500;              /* codice esadecimale */
  color: rgb(255, 165, 0);     /* rosso, verde, blu */
  color: rgba(255, 165, 0, 0.5); /* lo stesso, più la trasparenza (0 = invisibile, 1 = solido) */
}
```

Non ci sono molti colori con nome che valga la pena memorizzare oltre agli ovvi (`red`, `black`, `white`, `orange`...) &mdash; per qualcosa di più specifico, come l'arancione esatto del tuo gatto in particolare, ti servirà un codice esadecimale o un valore `rgb()`, di solito scelto con uno strumento selettore di colore piuttosto che indovinato.

`color` imposta il colore del *testo* nello specifico. Per lo sfondo di un elemento, c'è una proprietà diversa:

```css
.scatola-preferita {
  background-color: #d2b48c; /* color cartone */
}
```

## <a id="box-model" href="#box-model">#</a> Il box model

Ecco l'idea più importante di tutto il CSS: **ogni elemento su una pagina è una scatola.** Un paragrafo è una scatola. Un titolo è una scatola. Un'immagine è una scatola. Persino una singola parola racchiusa in uno `<span>` è una scatola. I gatti, guarda caso, questa cosa la capiscono già d'istinto &mdash; non hai mai visto un gatto confuso sul fatto se entri o meno in un contenitore.

Ogni scatola è fatta di quattro strati, dall'interno verso l'esterno:

```
+--------------------------------------+
|                margin                |
|  +---------------------------------+ |
|  |            border               | |
|  |  +----------------------------+ | |
|  |  |          padding           | | |
|  |  |  +----------------------+  | | |
|  |  |  |       content        |  | | |
|  |  |  +----------------------+  | | |
|  |  +----------------------------+ | |
|  +---------------------------------+ |
+--------------------------------------+
```

- **content** è il testo o l'immagine vera e propria.
- **padding** è lo spazio *dentro* la scatola, tra il contenuto e il suo bordo &mdash; pensalo come il morbido rivestimento interno di un trasportino.
- **border** è una linea visibile (o invisibile) attorno al padding &mdash; il trasportino stesso.
- **margin** è lo spazio *fuori* dalla scatola, che spinge via le altre scatole &mdash; quanto spazio personale il trasportino esige dalle scatole vicine.

```css
.scatola-preferita {
  padding: 20px;
  border: 2px solid brown;
  margin: 10px;
}
```

Ciascuno di questi quattro lati può anche essere impostato singolarmente &mdash; `margin-top`, `padding-left`, e così via &mdash; quando non vuoi che tutti e quattro i lati coincidano.

## <a id="text" href="#text">#</a> Testo e font

Una manciata di proprietà copre la maggior parte di quello che vorrai fare con il testo:

```css
h1 {
  font-family: "Helvetica", "Arial", sans-serif;
  font-size: 40px;
  font-weight: bold;
  text-align: center;
  line-height: 1.5;
}
```

- `font-family` è una *lista* di font in ordine di preferenza &mdash; il browser usa il primo che ha effettivamente installato, ripiegando via via sulla lista. Termina sempre la lista con una famiglia generica come `sans-serif` o `serif`, come rete di sicurezza.
- `font-size` e `font-weight` (quanto grassetto) sono abbastanza autoesplicativi.
- `text-align` sposta il testo a sinistra, a destra o al centro dentro la sua scatola.
- `line-height` controlla lo spazio tra le righe di testo &mdash; un po' di respiro, così come un gatto preferisce un po' di spazio tra sé e il bordo della scatola (finché non gli va più bene, e allora si piega in due per starci comunque dentro).

## <a id="display" href="#display">#</a> Display

Ogni scatola ha un tipo di `display`, che controlla come si comporta accanto alle altre scatole. I due che incontrerai di continuo:

- gli elementi **block** (come `<div>`, `<p>`, `<h1>`) partono sempre su una nuova riga e occupano tutta la larghezza disponibile, impilandosi uno sull'altro come scatole in un furgone dei traslochi.
- gli elementi **inline** (come `<span>`, `<a>`) stanno *dentro* una riga di testo, scorrendo insieme al resto del contenuto, occupando solo la larghezza di cui hanno bisogno.

```css
span {
  display: block; /* ora si comporta come un div, impilandosi su una riga tutta sua */
}
```

Puoi sovrascrivere il tipo di display predefinito di un elemento in qualsiasi momento, il che è una comoda via d'uscita quando il comportamento predefinito non è quello che ti serve.

## <a id="flexbox" href="#flexbox">#</a> Flexbox, in breve

Per disporre più scatole *una accanto all'altra*, in riga o in colonna, con spaziatura uniforme, il CSS moderno ti offre **flexbox**. Metti `display: flex` su un contenitore, e i suoi figli diretti si allineano automaticamente:

```css
.mensola-gatti {
  display: flex;
  justify-content: space-between; /* distribuisce i figli in modo uniforme */
  align-items: center;            /* li centra verticalmente */
}
```

```html
<div class="mensola-gatti">
  <div>Bill</div>
  <div>Tabby</div>
  <div>Gatto del Soffitto</div>
</div>
```

I tre gatti sopra ora stanno in una fila ordinata, spaziati uniformemente, invece di impilarsi uno sull'altro come farebbero i normali elementi block. Flexbox è un argomento intero a sé stante &mdash; questo basta solo per sapere che esiste e che problema risolve. [Flexbox Froggy](https://flexboxfroggy.com/) è un gioco davvero eccellente (e gratuito) per impararlo per bene.

## <a id="pseudo-classes" href="#pseudo-classes">#</a> Pseudo-classi

Una **pseudo-classe** dà stile a un elemento in base a uno *stato* in cui si trova, non a cosa è o a quale classe ha. La più comune è `:hover`, che si applica mentre il mouse punta su qualcosa:

```css
a:hover {
  color: red;
  text-decoration: underline;
}
```

Ora ogni link diventa rosso mentre il cursore ci sta sopra, e torna normale nel momento in cui se ne va &mdash; senza bisogno di JavaScript, il browser gestisce da solo la contabilità del "il mouse è lì in questo momento?". Altre pseudo-classi comuni includono `:first-child` (il primo elemento tra i suoi fratelli) e `:focus` (un campo attualmente selezionato per digitare).

## <a id="responsive" href="#responsive">#</a> Design responsive

Non tutti gli schermi hanno la stessa dimensione &mdash; una pagina deve avere un aspetto sensato sia su un monitor enorme *sia* su un telefono tenuto di traverso da un umano che ha l'altra mano occupata a reggere un gatto. Le **media query** permettono a un foglio di stile di applicare certe regole solo in determinate condizioni, più comunemente la larghezza dello schermo:

```css
.mensola-gatti {
  display: flex;
}

@media (max-width: 600px) {
  .mensola-gatti {
    display: block; /* impila verticalmente sugli schermi stretti */
  }
}
```

Le regole dentro `@media (max-width: 600px) { ... }` si applicano solo quando la finestra del browser è larga 600 pixel o meno. Questa è l'intera base del "design responsive" &mdash; scrivi prima i tuoi stili normali, poi aggiungi delle eccezioni per gli schermi stretti.

## La fine!

Questo è abbastanza CSS per impedire a una pagina di sembrare un modulo governativo. C'è molto altro là fuori &mdash; animazioni, layout a griglia, proprietà personalizzate, trasformazioni &mdash; ma ora hai le vere fondamenta su cui è costruito tutto il resto: i selettori scelgono le cose, le dichiarazioni le descrivono, e la specificità decide chi vince quando due regole sono in disaccordo.

Hai un altro argomento che vorresti veder trattato? Apri una issue [su GitHub](https://github.com/lucanenni/css-for-cats-it/issues).

### <a id="recommended-reading" href="#recommended-reading">#</a> Letture consigliate

- La [guida CSS di MDN](https://developer.mozilla.org/it/docs/Web/CSS) è il miglior riferimento per ogni proprietà e valore esistente.
- [Flexbox Froggy](https://flexboxfroggy.com/) e [Grid Garden](https://cssgridgarden.com/) trasformano l'esercizio sul layout in dei veri e propri giochi.
- [CSS-Tricks](https://css-tricks.com/) (in inglese) ha ottime guide su quasi ogni argomento CSS, inclusa [la guida classica a Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).
- [HTML per Gatti](https://github.com/lucanenni/html-for-cats-it), se non l'hai già letto, per lo scheletro su cui va questo pelo.
- [JavaScript for Cats](https://github.com/max-mapper/javascript-for-cats) di [@maxogden](http://twitter.com/maxogden) (o la sua [traduzione italiana](https://github.com/lucanenni/javascript-for-cats-it)), per quando vorrai che le tue scatole facciano davvero qualcosa.

<hr>

*CSS per Gatti è un progetto indipendente di fan, scritto per l'universo di [JavaScript for Cats](https://github.com/max-mapper/javascript-for-cats) di [@maxogden](http://twitter.com/maxogden), con affetto e senza alcuna affiliazione ufficiale. Contributi e correzioni sono benvenuti su [GitHub](https://github.com/lucanenni/css-for-cats-it).*

*Nota di manutenzione (14/08/2026): aggiornate le dipendenze di build (`marked`, `mustache`) per correggere vulnerabilità di sicurezza note (ReDoS in `marked`, XSS in `mustache`); adeguato `render.js` alla nuova API di `marked`. Nessuna modifica al contenuto del tutorial.*
