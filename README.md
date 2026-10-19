# STEPA

React + JavaScript aplikacija sa Vite-om, spremna za Vercel. Potreban je Node.js 24.x.

## Lokalni razvoj

```powershell
npm.cmd run dev
```

Otvori adresu koju terminal prikaze (obicno http://localhost:5173).
Pocetna komponenta je `src/App.jsx`, stilovi su u `src/App.css` i `src/index.css`.
Staticke fajlove stavljaj u `public/`.

```powershell
npm.cmd run lint
npm.cmd run build
npm.cmd run preview
```

Build pravi produkcionu verziju u `dist/`, a preview je pokrece lokalno.
Na sistemima bez PowerShell ogranicenja mozes koristiti `npm` umesto `npm.cmd`.
Na drugom racunaru instaliraj zavisnosti komandom `npm.cmd ci`.

## Vercel

1. Postavi projekat u svoj Git repozitorijum.
2. Na Vercel-u izaberi Add New Project i uvezi repozitorijum.
3. Root Directory je ovaj folder. Framework: Vite. Build Command: `npm run build`. Output Directory: `dist`.
4. Pokreni Deploy.

`vercel.json` sadrzi build podesavanja i SPA fallback za direktno otvaranje frontend ruta.
Projekat jos nije objavljen niti povezan sa Vercel nalogom.

## Environment promenljive

Kopiraj `.env.example` u `.env.local` ako su ti potrebne promenljive.
Koristi `VITE_` prefiks i pristupaj im kroz `import.meta.env.VITE_IME`.
Ove vrednosti su javne u browseru; tajni kljucevi pripadaju backendu.
Za deploy dodaj vrednosti u Vercel Project Settings > Environment Variables.

Dokumentacija: [Vite](https://vite.dev/guide/), [React](https://react.dev/), [Vercel](https://vercel.com/docs/frameworks/frontend/vite).

## Pregled rodjendanskog ekrana

Dok radi `npm.cmd run dev`, otvori adresu sa `?preview=birthday`
(npr. http://localhost:5173/?preview=birthday).
Ovaj pregled radi samo u razvojnom rezimu; produkcija ceka datum rodjendana.

Slika se uvozi iz `images/srecan_rodj_andjela.png`.
Zvuk je izdvojen iz `images/stepa.mkv` u `images/stepa.mp3` (ceo dostavljeni isecak, bez petlje).
Komponenta `src/BirthdayMusic.jsx` pusta samo MP3; video se ne ucitava niti prikazuje.
Klik na dugme CLICK HERE! iznad slike pokrece pesmu jednom.
Dugme nestaje kada reprodukcija pocne; nema kontrola za pauziranje ili ponavljanje.
Osam sekundi nakon pocetka reprodukcije otvara se uvodni ekran igre (`src/GameIntro.jsx`).
Klik na KLIKNI ZA POKLON otvara memory igru: 5 parova / 10 kartica.
Koriste se `images/memory1.jpg`, `memory3.jpg`, `memory4.jpg`, `memory5.jpg` i `memory6.jpg`.
Zavrsi igru otvara jedan prozor: Nastavi igru, Druga igra, Pocetna strana.
Nastavi cuva trenutnu rundu, Druga igra otvara drugu igru sa novim rasporedom, Pocetna strana vraca na rodjendansku sliku sa CLICK HERE dugmetom.
Posle memory pobede rezultat ostaje vidljiv; tek klik na Dalje otvara pitanje o prelasku na drugu igru.
Da otvara slagalicu, a Ne vraca na rodjendansku sliku sa CLICK HERE dugmetom.
Svaka nova runda obe igre nasumicno mesa delove/kartice.
Pogresan par se zatvara posle sekunde. Nakon svih parova prikazuje se BRAVO i broj poteza.
Drugi poklon je slagalica 3x3 sa slikom `images/stepin_vajat.jpg`.
Klik na dva dela menja njihova mesta; cilj je vratiti svih 9 delova na pravo mesto.
Posle slagalice sastavljena slika ostaje vidljiva uz rezultat, Nova runda i Pocetna strana, bez automatskog prozora.
YouTube se vise ne koristi. FFmpeg je koriscen samo za izdvajanje zvuka i nije potreban za pokretanje ili deploy.
