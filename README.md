# Workshops de IA aplicada

Sitio en Hugo con el tema [Hextra](https://imfing.github.io/hextra/), publicado en GitHub Pages.

## Estructura

- `content/introductorio/`: curso introductorio
- `content/avanzado/`: curso avanzado

Cada sesión es una carpeta (page bundle) dentro de su curso:

```
content/<curso>/NN-tema/
├── index.md     # notas de la sesión (weight = orden en el sidebar)
├── slides.md    # presentación reveal.js; las diapositivas se separan con ---
└── ...          # notebooks y datos que se publican junto a la sesión
```

Si una sesión tiene presentación, su `index.md` lleva `outputs: [html, slides]`. Así Hugo genera `slides.html` desde `slides.md`.

## Desarrollo local

Requiere Hugo extended ≥ 0.146.

```sh
git submodule update --init --recursive
hugo server
```
