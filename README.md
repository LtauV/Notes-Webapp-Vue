# vue-notesModal-tuto
This is a web app that allows you to take notes and display their content and date of creation in a little card

The content is stored in the LocalStorage of your browser. If you want to delete your history of notes, either clear the cache of your browser, or type localStorage.clear() in the dev console of your browser

## Known Issues : 
- When the inputed text is too long, it won't fit on the card
- If your browser has a global dark theme, the script that generates random colors will often make unreadable colors
- Date is in a very weird format when data is imported from the local storage
- notes IDs are randomly generated, but there is a 1 over 1 million chance to have the same Id twice
- responsiveness is limited but "works" on standard phone sizes

#

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
