---
layout: post
title: Conosciamo le API di telegram usando python
---

**Telegram** è un app di messagistica istantanea simile a whatsapp, ad alcuni tratti migliore, ma non voglio perdermi in inutili discorsi. La differenza sostanziale è che Telegram permette di chattare con dei **bot**.

## Cosa è un bot?

Un bot è una chat con un servizio pre-programmato, che risponde in maniera diversa a seconda del testo che gli mandi. Detto così può sembrare inutile, ma ci sono bot che si connettono a dei servizi online, come la mappa dei defribillatori, oppure bot che permettono di effettuare dei pagamenti.

## Come si crea un bot?

Per creare un bot, bisogna usare un altro bot. Digitiamo nel campo di ricerca **@botfather** e clicchiamo su avvia.


Ora digitiamo il comando `/newbot` e seguiamo le indicazioni del bot. Al termine ci darà un codice, detto TOKEN, che ci da l'accesso alle API di Telegram. Conserva quel codice per dopo.

## La libreria Telepot

Prima di passare alla vera e propria programmazione del nostro bot telegram, proviamo alcune funzioni della libreria **telepot** con le API di Telegram.\\Avete conservato il vostro TOKEN? Ora ci servirà!

Prima di tutto installiamo pip, se non lo avete già scaricato. Apriamo una pagina nel terminale e digitiamo:

```bash
~$ sudo apt install python-pip
```

Ora installiamo la libreria telepot:
```bash
~$ pip install telepot
```

Siamo finalmente pronti a far funzionare il nostro primo bot. Nel nostro terminale digitiamo il comando `python`, che restituirà la seguente schermata:

```bash
~$ python
Python 2.7.12 (default, Nov 19 2016, 06:48:10)
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
La prima api che vedremo, verificherà che il nostro bot è funzionante. Si chiama `getMe()`. Nell'interprete python scriviamo:
```python
>>> import telepot
>>> bot = telepot.Bot('TOKEN')
>>> bot.getMe()
{u'first_name': u'NOME_DEL_BOT', u'id': BOT_ID, u'username': u'USERNAME_DEL_BOT'}
```
Che restituirà un JSON contenente le informazioni sul bot. Miraccomando! Sotituite TOKEN con il  vostro token!\\ Sappiamo ora come la funzione getMe() ritorni le informazioni sul bot. MA coem fa il bot a ricevere  nostri messaggi? Per questo ci viene incontro l'altra API che vedremo, `getUpdates()`. Vediamone il funzionamento:
```python
>>> from pprint import pprint
>>> resp = bot.getUpdates()
>>> pprint(resp)
[{u'message': {u'chat': {u'first_name': u'NOME_UTENTE',
                         u'id': ID_UTENTE,
                         u'last_name': u'COGNOME_UTENTE',
                         u'type': u'private'},
               u'date': 8309039848,
               u'from': {u'first_name': u'NOME_UTENTE',
                         u'id': ID_UTENTE,
                         u'last_name': u'COGNOME_UTENTE'},
               u'message_id': 13,
               u'text': u'TESTO_MESSAGGIO'},
  u'update_id': NUM_MESS}]
```

Analizziamo il seguente codice:\\
La funzione pprint, stampa semplicemente in maniera leggibile il JSON del getUpdates. Creiamo una variabile di nome resp, e dentro ci mettiamo il contenuto della richiesta `getUpdates()`, e infine la stampiamo. Semplice no? Dentro il messaggio, notiamo diverse informazioni, che dovremo tenere a mente quando andremo a sviluppare il nostro bot. il più importante è l'`id`, che identifica la chat tra l'utente e il bot.
\\
\\
Vi è piaciuto questo post? Avete qualcosa da suggerirmi? Commentate qui sotto! A presto con la continuazione del tutorial!
