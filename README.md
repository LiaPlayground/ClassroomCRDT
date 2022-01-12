<!--
author:   André Dietrich

email:    andre.dietrich@informatik.tu-freiberg.de

version:  0.0.1

language: de

narrator: US English Female

-->

# Verteilte Klassenräume

__Problemstellung:__

* kein zentrale Server
* kleine Gruppen
* offline First (Verbindungsabbrüche)
* Datenhoheit
* Annonymität

## Web 3.0

* ~Semantic Web~
* Progressive Web Apps (PWAs)
* Distributed Apps (DApps)

  {{1}}
  - Etherium
  - BitCoin

    {{2}}
  - Browser:
    - WebRTC
    - IPFS
    - Hyperdat
    - Tor & onion

## CRDTs

**Conflict Free Replicated Data Types**

**Strong Eventual Consistency**

**Mathematisch beweisbar**

### Grundlage

**ACID 2.0**

{1}{ Assoziativ }
{2}{ Kommutativ }
{3}{ Idempotenz }
{4}{ Distributed ... irgendwas }

### Beispiel: Zähler

**Addition:**

    {{1}}
$$(1+2) + 3 = 1 + (2 + 3)$$

    {{2}}
$$1 + 2 = 2 + 1$$

    {{3}}
$$1+1 \neq 1$$

### Mengen: $\cup$

**Vereinigung**

    {{1}}
$$\Big(\{1\} \cup \{2\}\Big) \cup \{3\} =  \{1\} \cup \Big( \{2\} \cup \{3\}\Big)$$

    {{2}}
$$\{1\} \cup \{2\} = \{2\} \cup \{1\}$$

    {{3}}
$$\{1\} \cup \{1\} = \{1\}$$

### Problem: **D**

    {{1}}
```````````````
               "{a:3}"             "{a:3,b:5}"
Alice        -----o---         ---------*--------> "Summe = 8 "
                   \     ^       \     ^
                    v   /         v   /
Bob   ---------------*-o-----------*-o-----------> "Summe = 8 "
       "{b:5}"   "{a:3,b:5}"   "{a:3,b:5}"
```````````````

    {{2}}
* Operation based CRDT
* State based CRDT

## LiaScript: State based CRDT

**Was wird ausgetauscht?**

* Globaler Zustand (_Join_)
* Lokaler Zustand (_Update_)


## Backends & GlueCode

* Beaker & Hyperdat - Peer To Peer
* PubNub - Publish-Subscribe
* GunDB - Verteilte p2p Datenbank
* JitSi - WebRTC
* Matrix - ...

## Demo

### Umfragen

#### Texteingaben

**Wordcloud**

    [[___]]

**Sammlungen**

    [[___ ___]]

#### Vektoren

**Single-Choice**

    [(1)] Option 1
    [(2)] Option 2
    [(3)] Option 3

**Multiple-Choice**

    [[4]] Option 4
    [[5]] Option 5
    [[6]] Option 6

#### Matrizen

**Single-Choice**

    [(gut 1)(mittel 2)(schlecht 3)]
    [                             ] Option 1
    [                             ] Option 2
    [                             ] Option 3


**Multiple-Choice**

    [[1 gut][2 mittel][3 schlecht]]
    [                             ] Option 1
    [                             ] Option 2
    [                             ] Option 3


### Quizze

#### Einfach

What is $37 + 15$?

    [[52]]
    <script output="quiz:37+15">
      if ("@input" == "52") {
        true
      } else {
        "@input"
      }
    </script>

<script style="display: block">
//   3(7)       (3)7
// + 1(5)     + (1)5       The first and second steps were correct,
// ------ ->  ------  ->   but the student forgot to carry the 1
//   (12)       (4)2       in the 10 digit column.

if ("@input(`quiz:37+15`)" == "42") {
  send.liascript(`## Maybe you forgot to carry...

Checkout the follow video to recap carrying.

!?[Carrying for larger digits](https://www.youtube.com/watch?v=VPsYRPdlIpU)
`)
} else ""
</script>


<script style="display: block">
//   3(7)       (3)7       The first and second steps were also
// + 1(5)     + (1)5       correct, but carrying was not provided
// ------ ->  ------  ->   properly, maybe there is a problem with
//   (12)      (4)12       understanding digit columns...


if ("@input(`quiz:37+15`)" == "412") {
  send.lia(`You are nearly there, there might be a problem with the 10 digit columns...`)
} else ""
</script>


#### Komplex

Man or woman is obvious, but you guess the remaining German grammatical genders?

    [[male (der<!-- class="notranslate"-->)]   (female [die<!-- class="notranslate"-->])   [neuter (das<!-- class="notranslate"-->)]]
    [    [X]           [ ]             [ ]     ]  Mann<!-- class="notranslate"--> - German for man
    [    ( )           (X)             ( )     ]  Frau<!-- class="notranslate"--> - German for woman
    [    [X]           [ ]             [ ]     ]  Junge<!-- class="notranslate"--> - German for boy
    [    ( )           ( )             (X)     ]  Mädchen<!-- class="notranslate"--> - German for girl
    [    [X]           [X]             [ ]     ]  Paprika<!-- class="notranslate"--> - German for bell pepper
    [    (X)           (X)             (X)     ]  Joghurt<!-- class="notranslate"--> - German for yogurt

## Todo

* Update der LiaScript internen Strukturen (Service-orientiert)
* Implementierung eines Rechte- "Hierarch"-management
* CRDT-Trees für kollaboratives editieren
