# Fliper: lokalni model protiv clouda

Pokus za Bug: isti zadatak, napisati fliper koji radi u browseru, dobili su lokalni jezični model na laptopu i Claude u oblaku. Uzor je bila igra Pinball Deluxe: Reloaded (Made of Bits, 2017.), tema stola je naša: jadranski svjetionik noću.

**Igraj:**

- [Lokalni model (Qwen3.8-Flash-Next)](local/)
- [Cloud (Claude Opus 5.5)](cloud/)

Kontrole: Enter nova igra, Left Shift / Z / lijeva strelica lijevi fliper, Right Shift / / / desna strelica desni fliper, Space ili strelica dolje opruga (drži pa pusti), P pauza.

## Kako je rađeno

- Oba modela dobila su isti [prompt](PROMPT.md): jedan HTML fajl, bez biblioteka, sve se crta na canvasu, zadana fizika, pravila i kontrole.
- Grafiku (podlogu stola i zid) generirao je lokalno ComfyUI s modelom FLUX.2 Klein 4B. Kod crta sve fizičke dijelove stola preko nje.
- Računalo: Asus ProArt P16 s NVIDIA RTX Spark (N1X), 128 GB memorije, od toga 96 GB dodijeljeno GPU-u.
- Kod nismo ručno mijenjali ni u jednoj verziji.

## Lokalni model

- Qwen3.8-Flash-Next, kvantizacija IQ3_XXS (70,6 GB), llama.cpp b11401, kontekst 64k, oko 30 tokena u sekundi.
- S preporučenom razinom razmišljanja (xhigh) i sa srednjom (medium) model je dvaput potrošio svih 64k konteksta na razmišljanje i nije napisao kod (34 i 36 minuta). Uspio je tek s razinom low.
- Tri kruga: nakon svakog smo igru isprobali i modelu opisali što ne radi, bez savjeta kako to popraviti. Ukupno 54,7 minuta generiranja.
- Rezultat: kuglica izlazi u polje i fliperi je odbijaju, ali prepreke u donjem dijelu stola je zarobe. Igra nije igriva. Ovdje je verzija iz trećeg, zadnjeg kruga.

## Cloud

- Claude Opus 5.5 kao agent u Claude Codeu, jedan pokušaj, bez browsera i bez naših povratnih informacija. Smio je samo provjeriti sintaksu JavaScripta.
- 11,7 minuta do gotovog fajla.
- Rezultat: igriv iz prvog pokušaja.

To je jedan zadatak s jednim pokušajem po modelu, dakle primjer, a ne mjerilo.
