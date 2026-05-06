# Pagina contatti — Dott.ssa Miriam (psicoterapeuta)

Landing page mobile-first per portachiavi NFC con biglietto da visita digitale. Avvicinando il chip al telefono si apre questa pagina; il bottone **"Salva contatto"** genera al volo un file `.vcf` con tutti i dati e li passa direttamente in rubrica.

## File

- `index.html` — la pagina (singolo file, nessuna dipendenza esterna)
- `foto.jpg` (opzionale) — foto profilo

## Come modificare i dati

Apri `index.html` con un editor (Notepad, VS Code, anche Blocco note va bene) e cerca i punti seguenti.

### 1. Foto profilo

Cerca:
```html
<div class="avatar" id="avatar">
  <span>MC</span>
</div>
```

Sostituisci con:
```html
<div class="avatar" id="avatar">
  <img src="foto.jpg" alt="">
</div>
```

E carica `foto.jpg` nella stessa cartella. Consigliata: quadrata, almeno 256×256 px.

Se preferisci tenere il monogramma, basta cambiare le iniziali: `<span>MC</span>` → es. `<span>MR</span>`.

### 2. Nome, titolo, specializzazione, albo

Cerca queste righe nell'header:

```html
<div class="role-tag">Psicoterapeuta</div>
<h1 class="name">
  <span class="salutation">Dott.ssa</span>
  Nome Cognome
</h1>
<p class="subtitle">Specialista in psicoterapia<br>cognitivo-comportamentale</p>
<p class="albo">Albo Psicologi · n° 00000 · Lazio</p>
```

Sostituisci ogni placeholder con i dati reali. Il `<br>` nello `subtitle` è solo un'andata a capo.

### 3. Contatti (telefono, email, WhatsApp, indirizzo)

| Cosa | Cerca | Modifica |
|---|---|---|
| Telefono | `href="tel:+393331234567"` | numero senza spazi, con prefisso |
| Numero visualizzato | `+39 333 123 4567` | come vuoi che appaia |
| Email | `href="mailto:nome.cognome@email.it"` | l'email reale |
| Email visualizzata | `nome.cognome@email.it` | la stessa |
| WhatsApp | `href="https://wa.me/393331234567"` | numero **senza +** né spazi |
| Indirizzo (link Mappe) | `href="https://maps.apple.com/?q=Via+Esempio+1,+Roma"` | sostituisci con `Via+Tua+1,+Citta` (spazi = `+`) |
| Indirizzo visualizzato | `Via Esempio 1<br>00100 Roma (RM)` | come deve apparire |

### 4. Quote / frase d'accoglienza

Cerca:
```html
<div class="about">
  Uno spazio di ascolto, accoglienza e cura per ritrovare equilibrio e benessere.
</div>
```
Cambia il testo come preferisci.

### 5. Servizi offerti

Cerca la sezione `<div class="services">`. Ogni voce è un blocco `<div class="service">` con un nome e una descrizione. Aggiungi, rimuovi o modifica i blocchi liberamente — basta copiare un blocco esistente per aggiungerne uno.

### 6. Footer

```html
Dott.ssa Nome Cognome · P.IVA 00000000000
```

### 7. ⚠️ Dati della vCard (Salva contatto)

**Importantissimo**: i dati visualizzati nella pagina e quelli salvati nel `.vcf` sono **due cose separate**. Devi modificarli **entrambi**.

In fondo al file, dentro `<script>`, trovi:

```javascript
const vcfData = {
  firstName: 'Nome',
  lastName: 'Cognome',
  title: 'Psicoterapeuta',
  org: 'Studio di Psicoterapia',
  phone: '+393331234567',
  email: 'nome.cognome@email.it',
  website: 'https://example.com',
  street: 'Via Esempio 1',
  city: 'Roma',
  zip: '00100',
  region: 'RM',
  country: 'Italia',
  note: 'Albo Psicologi Lazio n° 00000 · P.IVA 00000000000'
};
```

Modifica ogni campo con i dati reali. Sono i campi che finiranno in rubrica quando il paziente tocca "Salva contatto".

### 8. Titolo della scheda browser

In alto:
```html
<title>Dott.ssa [Nome Cognome] — Psicoterapeuta</title>
```

## Pubblicare su GitHub Pages

1. Su [github.com](https://github.com) → **New repository** → nome es. `miriam-contatti` → spunta **Public** → **Create**
2. **"uploading an existing file"** → trascina `index.html` (e `foto.jpg` se la usi)
3. Commit
4. **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**
5. Dopo ~1 minuto online su `https://TUOUSER.github.io/miriam-contatti/`

## Programmare il chip NFC del portachiavi

App **NFC Tools** (Android Play Store / iOS App Store, gratis):

1. Apri NFC Tools → **Scrivi** → **Aggiungi un record**
2. Tipo: **URL/URI**
3. Incolla `https://TUOUSER.github.io/miriam-contatti/`
4. **Scrivi** e avvicina il portachiavi al telefono

Quando un paziente avvicina il telefono al portachiavi → si apre la pagina → tap su "Salva contatto" → tutto in rubrica con un gesto.

## Note

- La pagina funziona offline una volta caricata, è 100% statica
- Il `.vcf` è generato dal browser al volo (non c'è bisogno di hostare un file separato)
- Compatibile sia con iPhone che Android — la vCard è in formato standard 3.0
