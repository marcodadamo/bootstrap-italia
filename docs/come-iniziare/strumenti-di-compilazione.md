---
layout: docs
title: Strumenti di compilazione
description: Come compilare il codice sorgente e generare la documentazione che stai leggendo
group: come-iniziare
toc: true
---

{% capture callout %}
**Questa pagina è destinata a chi desidera personalizzare la libreria.**

Di seguito si possono trovare gli strumenti per personalizzare e ricompilare i file sorgente di Bootstrap Italia, oltre a poter generare la documentazione che stai leggendo in un ambiente di sviluppo locale. Le informazioni di seguito non sono indispensabili per l'utilizzo di Bootstrap Italia come libreria. In tal caso ti può essere utile la [pagina introduttiva]({{ site.baseurl }}/docs/come-iniziare/introduzione/).
{% endcapture %}{% include callout.html content=callout type="info" %}

## Compilare la libreria

Il tema Bootstrap Italia, così come Bootstrap 4 stesso, usa script `npm` per la compilazione dei file (è ovviamente possibile usare `yarn` in alternativa). Per rendere operativo il sistema di compilazione di Bootstrap Italia, è necessario:

1. Clonare attraverso GIT o scaricare l'intero repository in una cartella sul proprio computer.
2. [Scaricare e installare Node.js](https://nodejs.org/download/), che è necessario per gestire le dipendenze attraverso `npm` o `yarn`.
3. Verificare che i comandi siano disponibili provando a lanciare `node -v` e `npm -v`.
4. Dalla cartella del progetto, lanciare il comando `npm install` per installare le dipendenze descritte nel file [package.json]({{ site.repo }}/blob/master/package.json).

### Script di compilazione

Il file [package.json]({{ site.repo }}/blob/master/package.json) include il seguente comando, che fa uso di  **[SASS][sass], [Autoprefixer][autoprefixer], e [UglifyJS][uglify]** per la compilazione dei file sorgente di Bootstrap Italia:

`npm run build`

Tale comando crea una cartella `/dist`, dove vengono pubblicati i file compilati da utilizzare nelle proprie pagine HTML.

Per iniziare a modificare la libreria, la cartella d'interesse è `/src`, che contiene tutti i file sorgente, e in particolare i file:

- `/src/scss/bootstrap-italia.scss`
- `/src/js/bootstrap-italia.js`

## Compilare la documentazione

La documentazione di Bootstrap Italia è gestita con [GitHub Pages](https://pages.github.com/) attraverso [Jekyll][jekyll]: per questo è composta di file statici che risiedono sul branch `gh-pages`. I file presenti a questo branch corrispondono esattamente ai file generati con il comando `bundle exec jekyll build` nella cartella locale `_gh-pages`.

Per poter generare e testare la documentazione in ambiente locale, è necessario: 

1. Installare [Ruby][install-ruby]*, che renderà disponibile il comando `gem install *`.
2. Lanciare il comando `gem install bundler` per installare [Bundler][gembundler].
3. Lanciare il comando `bundle install`. Questo comando, in modo simile a quanto avviene per `npm install` si occuperà di installare tutte le dipendenze Ruby come descritto nel file [Gemfile]({{ site.repo }}blob/master/Gemfile); in questo caso Jekyll e i suoi plugin.

\* **Utenti Windows:** è bene seguire [questa guida][jekyll-windows] per installare Jekyll senza problemi.
  
Sono inoltre disponibili maggiori informazioni su Jekyll a [questa pagina][jekyll].

### Script di compilazione

Il comando

`npm start`

avvia due azioni: la compilazione dei file sorgente (come visto al paragrafo precedente), e l'esecuzione del comando `bundle exec jekyll build`. Oltre a questo, lancia un server locale e si mette in ascolto di ogni modifica ai file per:
- ricompilare i file sorgente Javascript/SASS
- ricompilare i file della documentazione (principalmente in formato Markdown)
- rendere disponibile all'indirizzo `http://127.0.0.1:4000/` e ricaricare automaticamente la documentazione

La struttura delle cartelle della documentazione è la seguente:

- `_data`: assieme al file `config-yml` definiscono le variabili utilizzate nei vari template ([documentazione][jekyll-data])
- `_includes`: contiene porzioni di codice HTML ([documentazione][jekyll-includes])
- `_layouts`: definisce alcuni modelli di pagina ([documentazione][jekyll-themes])
- `_plugins`: contiene funzioni che aumentano le funzionalità di Jekyll ([documentazione][jekyll-plugins])
- `docs`: è la cartella principale dove risiede la documentazione in formato Markdown.
- `docs/assets`: contiene file statici (javascript, css e immagini) necessari al buon funzionamento della documentazione. **Non sono file compilati nella libreria finale Bootstrap Italia**.

## Pubblicare la documentazione

Per pubblicare la documentazione, prima di tutto è necessario generare i file statici nella cartella d'appoggio `_gh_pages`. Per fare questo, è necessario portare tutto il contenuto di tale cartella sul branch `gh-pages` con il comando:

`npm run documentation-deploy-to-gh-pages`

Tale comando creerà _automagicamente_ un nuovo commit sul branch `gh-pages` del repository remoto su cui si sta lavorando, lanciando così la pubblicazione immediata della documentazione
su GitHub Pages e visibile all'indirizzo [https://italia.github.io/bootstrap-italia/](https://italia.github.io/bootstrap-italia/).

[bootstrap-themes]: https://getbootstrap.com/docs/4.0/getting-started/theming/
[autoprefixer]: https://github.com/postcss/autoprefixer
[uglify]: https://github.com/mishoo/UglifyJS2
[sass]: http://sass-lang.com/
[install-ruby]: https://www.ruby-lang.org/en/documentation/installation/
[gembundler]: https://bundler.io/
[jekyll]: https://jekyllrb.com/docs/home/
[jekyll-windows]: https://jekyllrb.com/docs/windows/#installation-via-rubyinstaller
[jekyll-data]: https://jekyllrb.com/docs/datafiles/
[jekyll-includes]: https://jekyllrb.com/docs/includes/
[jekyll-themes]: https://jekyllrb.com/docs/themes/
[jekyll-plugins]: https://jekyllrb.com/docs/plugins/

## Creare una nuova release

Per aggiornare il numero di versione e creare una nuova release, al momento è necessario effettuare i seguenti passi manuali:

* Aggiornamento numero di versione in formato semver x.x.x su file `package.json` e `_config.yml`
* Lanciare i comandi `npm run build && npm run documentation-build`
* Lanciare il comando `npm i` per aggiornare il file `package.lock`
* Commit e push delle modifiche
* Tag del commit con numero di versione in formato semver x.x.x
* Creazione manuale di un file compresso `bootstrap-italia.zip` della cartella `/dist`
* Scrivere le release notes su GitHub e allegare il suddetto file compresso
* `npm publish` per aggiornare la versione su `npm`

---

###### Continua la lettura >

Se ti interessa sapere come modificare o aggiungere nuovi componenti alla libreria Bootstrap Italia,
continua a leggere alla [pagina che spiega come farlo]({{ site.baseurl }}/docs/come-iniziare/modificare-componenti/).
