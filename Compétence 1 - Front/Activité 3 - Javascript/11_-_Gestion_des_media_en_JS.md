# La gestion des médias en JS

## Rappels

HTML propose deux balises pour manipuler des fichiers multimédias : <audio> et <video>.

Javascript permet d'interagir avec ces deux éléments, ou de réagir à des actions de l'utilisateur sur ces éléments.

## Sommaire

  1. Propriétés et méthodes des éléments média
  2. Gestion des événements
  3. getUserMedia()

## 1. Propriétés et méthodes des éléments média

Les éléments média ont des propriétés et méthodes pour contrôler la lecture, le volume, etc.

  * Lecture et pause : 

```js
.play()
.pause()
```

  * Propriétés de contrôle :

```js
.currentTime
.duration
.volume
.muted
.paused
.ended
.seeking
```

  * Gestion des sources :

```js
.src
.currentSrc
.canPlayType(type)
```

## 2. Gestion des événements

Liste des événements courants survenant sur les médias HTML :

```js
'play'
'pause'
'ended'
'timeupdate'
'volumechange'
'seeking'
'seeked'
```

Il est possible d'écouter ces différents événements avec un addEventListener() classique.

## 3. getUserMedia()

La méthode getUserMedia() de l'objet navigator.mediaDevices permet d'accéder aux périphériques media du navigateur de l'utilisateur : webcam, micro, etc.

Vous pouvez retrouver sa description sur le [MDN](https://developer.mozilla.org/fr/docs/Web/API/MediaDevices/getUserMedia), avec des exemples d'utilisation.