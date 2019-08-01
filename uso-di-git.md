# || Come si usa GIT ||

1. Tutto avviene usando un terminale: sospetto la procedure sia identica su un Mac, l'unica cosa che potrebbe cambiare è come
   reperire GIT (su una macchina \*nix:

```
$ sudo apt-get install git
```

).

2. La procedura per "clonare" un repository come copia locale sulla propria macchina è:

. avere un account
. avere il permesso di cincionare con la repo
. dare, nella cartella dove volete creare la sottocartella "repo_dello_gnogni", il comando da terminale:

```
git clone https://[[vostro_nome_utente]]@bitbucket.org/killing_buddha/repo_dello_gnogni.git
```

3. L'uso di GIT è abbastanza semplice:

. PRIMA DI INIZIARE A MODIFICARE ALCUNCHÉ, aggiornate sempre la vostra copia locale alla versione più recente
(l'ultimo commit che è stato fatto) dando il comando

`$ git pull`

. lo dico meglio: AGGIORNATE SEMPRE LA VOSTRA COPIA LOCALE PRIMA DI INIZIARE A MODIFICARE ALCUNCHÉ. Questo evita
di creare dei conflitti (che a volte, anche se GIT è molto intelligente, non si riescono a risolvere se non perdendo molto tempo.)
Quando avete a disposizione la versione più recente della repository, il comando

`$ git status`

dovrebbe dirvi un rassicurante

    Sul branch master
    Your branch is up-to-date with 'origin/master'.
    nothing to commit, working directory clean

. Fate le modifiche che volete al file / ai file su cui lavorate: modificare testo, aggiungere un file
o cartella, cancellare un file o cartella, rinominarli, sono tutte operazioni ammesse.

. Una volta che avete terminato, o quando avete finito di fare una modifica importante,

`$ git add -A`

. Prima di dare questo comando, "git status" vi avrebbe avvertito della presenza di file, cartelle
o altro che sono state modificate, ma non aggiunte al "workbench" (il posto dove GIT vede il lavoro che poi committerete):

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   [[[nomefile]]]

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

    [[nomefile/cartella]]

no changes added to commit (use "git add" and/or "git commit -a")

Dopo aver ordinato

`git add -A`

invece, il comando "git status" dovrebbe dare come risultato

    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    	new file/folder:   [[nome]]
    	modified:   [[nome]]

. Ora dobbiamo committare le modifiche; fino a questo punto, il processo è reversibile, e se nel frattempo
altre modifiche che rendono le nostre obsolete sono state committate da altri utenti, possiamo decidere
quali tenere. Quello che GIT fa a questo punto è raccogliere dai vari workbench degli utenti tutte le modifiche
ai file che tiene nel repository, e confrontarle marcando le differenze (sempre che si siano create in
quel lasso di tempo: 999 volte su 1000 c'è solo un utente per volta che lavora sulla repo; in progetti
piccoli (<10 persone) non accadrà mai di lavorare allo stesso tempo e questo discorso si semplifica molto;
ma siccome valgono le leggi di Murphy...)

. Il comando

`$ git commit -m "[[[commento]]]"`

committa le modifiche. tra le virgolette c'è del testo che spiega cosa avete fatto; solitamente si scelgono
poche parole che lo dicono concisamente: "added thm 4.7", "modified Lemma 5", "created section 1.1"...

!!! É IMPORTANTE SPECIFICARE SEMPRE QUALCOSA COME COMMENTO (GIT NON ACCETTA COMMIT VUOTI).
Quando non modificate niente di importante, fate un esperimento, modificate una
parte commentata, o qualsiasi altra cosa di insignificante, la prassi è specificare uno
"standard commit" oppure "tua madre prende ancora banconote false".

Ora, "git status" restituisce

    [master 93f9ffc] [[[commento]]]
     2 files changed, 55 insertions(+), 4 deletions(-)
     create mode 100644 nome

Che significa che tutto va come deve.

. L'ultimo passo, per rendere definitive le modifiche è

`$ git push`

Fatto questo, sul repo vengono scritte le modifiche che avete apportato, le quali diventano
ufficiali (soprattutto, diventa possibile tornare a questa versione in qualsiasi momento
da una più moderna, se dovesse servire). GIT vi chiederà la password con cui avete creato
il vostro account; questo rende molto leggibile l'evoluzione del documento: tutti
i commit e i push sono tracciati con il vostro nome utente, un identificativo numerico, il
contenuto del commento ad ogni commit, e diverse altre informazioni

Pushate le modifiche, "git status" restituisce

    Counting objects: 5, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (5/5), 1.57 KiB | 0 bytes/s, done.
    Total 5 (delta 3), reused 0 (delta 0)
    To https://killing_buddha@bitbucket.org/killing_buddha/nome_del_repo.git
       46d4e3d..93f9ffc  master -> master
