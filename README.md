# MuntApp · InnovaMunt

Prototip web per a l’**EAP Adults La Muntanyeta** (Castelldefels): previsió de la demanda per a l’equip i accés directe dels pacients i les famílies al professional que els cal, sense traspassos.

> **Prototip de demostració amb dades fictícies.** No és un producte sanitari ni està connectat a cap sistema clínic. No hi introduïu dades reals de pacients.

**Demo:** https://jotamoga.github.io/muntapp/

**InnovaMunt (mòbil)**

| Inici | Qui sou? | Assistent | Enviat |
| --- | --- | --- | --- |
| ![Inici](docs/inici.png) | ![InnovaMunt](docs/innovamunt.png) | ![Assistent](docs/assistent-ia.png) | ![Enviat](docs/enviat.png) |

**MuntApp (web i mòbil)**

| Avui | Fitxa del pacient | Previsió |
| --- | --- | --- |
| ![Avui](docs/muntapp-avui.png) | ![Pacient](docs/muntapp-pacient.png) | ![Previsió](docs/muntapp-previsio.png) |

## Què és

Una sola pàgina web amb dues portes. El model és semblant a la eConsulta, però amb el seguiment dels programes de crònics integrat.

### InnovaMunt · pacients i famílies (pensat per al mòbil)

Un assistent pas a pas, amb una pantalla per decisió i barra de progrés:

1. **Usuari:** ICC, DM2, PCC, MACA o ATDOM.
2. **Motiu:** constants, problema de salut, medicació o tràmits.
3. **Detall:**
   - **Problema de salut:** l’assistent entén el text lliure («fa 5 dies que no fa caca») i proposa fins a 3 opcions amb el grau de confiança. També hi ha els problemes més habituals de cada perfil i 12 categories amb més de 45 problemes. Cada problema pregunta els seus signes d’alarma, amb foto opcional.
   - **Constants:** amb els últims valors ja posats i botons + i −.
   - **Medicació** i **tràmits:** pantalles pròpies.
4. **Destinatari:** infermeria, medicina, treball social o UAC, amb l’opció recomanada marcada.
5. **Enviar:** resum i un sol resultat gràfic (urgent 112, prioritat alta, revisar avui, rebut o tot correcte).
6. **Seguiment de la petició:** la família veu si l’han rebuda, qui l’ha assumit, quan la trucaran i quan s’ha resolt (també a «Les meves peticions»), amb consells d’autocura mentre espera i quan tornar a avisar.

### MuntApp · equip (web i mòbil)

- **Avui:** una sola pantalla per saber què passa. Tres blocs, cadascun amb el seu comptador i una sola acció per fila:
  - **Peticions de les famílies** (consultes noves, ordenades per urgència) → «Resolt».
  - **Alertes de constants** (valors fora de rang) → «Revisat».
  - **Sense seguiment:** famílies que han deixat de registrar. L’app els envia un recordatori automàtic i, si en 24 h no responen, avisa l’equip que cal trucar → «He trucat».
  - **Escalat dels signes d’alarma:** si la infermera referent no està disponible (domicilis, absència…), la petició arriba també a la seva **UBA mirall**; si ningú la «Assumeix» en 30 minuts, avisa tot el **microequip**. Els signes urgents avisen el microequip a l’instant. Quan algú l’assumeix, la resta deixa de rebre l’avís. El selector «Veure com a» mostra què li toca a cada infermera.
  - **Abans de l’alerta:** pacients encara dins de rang però amb una tendència que s’hi acosta (glucosa que puja, freqüència cardíaca que puja, menja menys…), per fer una trucada preventiva.
  - Tocar una fila obre la fitxa del pacient. Al peu, els pacients sense res pendent i l’historial de peticions ateses.
- **Pacients:** filtre per programa i cerca. Cada fila mostra l’estat, el motiu, la tendència i l’adherència.
- **Fitxa del pacient:** consultes pendents amb accions, gràfiques d’evolució de 28 dies amb els llindars d’alerta, calendari de registres, últims valors i cronologia d’incidències i consultes.
- **Previsió (agendes dinàmiques):** visites i minuts lliures per UBA i microequip, semàfor de càrrega, escenaris i ordre de suport. A cada tall, MuntApp dona indicacions que es retroalimenten:
  1. **Mig tall (14 h):** quina UBA de relleu obre forats i si la demanda creix respecte a la setmana anterior.
  2. **Final del dia (19.45 h):** proposta per a la setmana vinent (moure controls de crònics estables al dia amb menys càrrega), amb el botó «Aplicar».
  3. **Cada 2 setmanes:** recalibrar la plantilla de cada dia segons la tendència (menys crònics i més forats del mateix dia si creix; recuperar crònics si baixa).
  4. **Cada mes:** tendència de 4 setmanes i error de previsió, per revisar-ho amb l’equip (PDCA).
  Cada ajust aplicat mostra el seu efecte en la previsió i es pot desfer.
- **Motius IA:** textos lliures de les famílies. Si un motiu es repeteix 3 vegades o més en 30 dies, l’assistent proposa afegir-lo com a opció o crear-ne una de nova. L’equip decideix.
- **Recerca:** indicadors dels estudis de l’equip i seguiment per infermera referent.

## InnovaMunt, La Meva Salut i eOSS

InnovaMunt no vol ser una altra app. La eConsulta de La Meva Salut és la porta d’entrada de tot Catalunya, però és asíncrona i no pregunta signes d’alarma. eOSS (Hospital de Bellvitge) fa telemonitoratge excel·lent de la insuficiència cardíaca, liderat des de l’hospital. InnovaMunt aporta el que falta a l’atenció primària: tots els programes de crònics i el domicili, la infermera de la UBA i el microequip, el cuidador com a usuari i la connexió amb les agendes. Està pensat per integrar-se a La Meva Salut (HES) i conviure amb eOSS.

## Implantació per fases

| Fase | Contingut |
| --- | --- |
| 1 | Quadre de comandament amb dades corporatives disponibles (SISAP i explotacions de l’eCAP). |
| 2 | Talls automàtics a les 14 h i a les 19.45 h, amb validació de Sistemes d’Informació i del delegat de protecció de dades. |
| 3 | InnovaMunt: seguiment amb la família i recerca de l’equip. |

## Limitacions d’aquesta demo

- Totes les dades són fictícies i es generen en obrir la pàgina; es perden en recarregar-la.
- L’assistent de text lliure és un classificador de paraules clau (català i castellà) que simula el comportament d’un model d’IA. En una versió real caldria un model validat clínicament i la confirmació d’un professional.
- Els llindars d’alerta, els signes d’alarma i els destinataris són exemples a validar amb els protocols de l’equip.
- Les fotos no surten del dispositiu.

## Publicar-la amb GitHub Pages

1. Pugeu `index.html`, `README.md` i la carpeta `docs/` a l’arrel del repositori.
2. A **Settings → Pages**, a «Build and deployment», trieu **Deploy from a branch**, la branca `main` i la carpeta `/ (root)`.
3. Al cap d’un minut, la web és a `https://USUARI.github.io/NOM-DEL-REPOSITORI/`.

Accessos directes:

- `…/#innovamunt` obre directament InnovaMunt.
- `…/#muntapp` obre directament MuntApp.

## Estructura

```
index.html   La web completa (HTML, CSS i JavaScript en un sol fitxer)
README.md    Aquest document
docs/        Captures de pantalla
```

No necessita cap instal·lació ni servidor: només un navegador. Les fonts tipogràfiques es carreguen de Google Fonts; sense connexió, es fa servir la font del sistema.

## Autoria

Joan Mora García · Infermer d’atenció primària, CASAP Castelldefels.
Projecte de co-direcció de l’EAP Adults La Muntanyeta, 2026.
