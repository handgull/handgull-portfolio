---
title: "Appunti su angular 17"
description: "I miei appunti del corso di fabio biondi su angular 17"
publishDate: "24 Mar 2024"
tags: ["angular", "js", "frontend"]
---

## Angular essentials

### Creare un progetto standalone

```sh
npx -p @angular/cli@latest ng new angular-demo -S -s -t
```

di default ormai angular è standalone: permette quindi la creazione di progetti senza i moduli ma solo con i component

- `-s` dice ad angular di creare componenti con l'inline-style
- `-t` dice di creare componenti con il template inline (in un unico file)
- `-S` dice di non creare i files di test quando si crea un nuovo componente

> Per avviare il progetto il comando è `npm start` che lancia quello che è definito dal `package.json`, verosimilmente un `ng serve` con qualche parametro opzionale.

[Standalone projects cheatsheet](/res/angular_1_standalone_projects.pdf)

### Interpolation - Template Tags
