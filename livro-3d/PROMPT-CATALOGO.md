# Prompt — Motion graphic 3D para o catálogo de materiais

Copie o texto abaixo, preencha os campos entre [colchetes] e anexe as capas.

---

Quero aplicar o método "Perspective Book" (livro 3D em perspectiva com motion graphic) a todos os materiais do meu catálogo.

**Referência pronta:** use `livro-3d/index.html` do repositório `jonathan-WPS/Site-NFC-master` como modelo técnico e visual. Ele já tem o livro 3D (capa, lombada, borda de páginas, contracapa, sombra, brilho), a linha do tempo da animação e o modo de gravação `?record`. Não invente outra técnica: reaproveite essa estrutura.

## Materiais do catálogo

Para cada item, tenho (ou vou anexar):

| # | Arquivo da capa | Título | Subtítulo | Ano/série | Tipo (Livro do Professor / Aluno) | Autor(a) | Selos (ex.: Alinhado à BNCC) |
|---|---|---|---|---|---|---|---|
| 1 | [capa1.png] | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| 2 | [capa2.png] | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| … | | | | | | | |

Se algum campo estiver vazio, leia a informação na própria capa. Nunca invente dados que não estejam na capa ou na tabela.

## O que entregar

1. **Uma página por material** em `catalogo/<slug>/index.html` + `capa.jpg` (capa redimensionada para 1100 px de largura, JPG qualidade ~88).
2. **Dois vídeos MP4 por material**, de ~14 s, em `catalogo/<slug>/video/`:
   - `<slug>-horizontal.mp4` (1920×1080)
   - `<slug>-vertical.mp4` (1080×1920, para Reels e Stories)
   - [opcional: `<slug>-quadrado.mp4` (1080×1080, para o feed)]
3. **Uma página de catálogo** em `catalogo/index.html` com todos os livros em 3D numa grade. O livro gira ao passar o mouse ou tocar, e cada um leva à sua página. Sem vídeo nessa página, só CSS.
4. **Um template único** (`catalogo/_template.html` + script de geração) para que novos materiais entrem no catálogo só preenchendo os dados, sem copiar e colar HTML.

## Regras de design (por material)

- **Paleta tirada da própria capa:** extraia de 5 a 7 cores dominantes (fundo, cor principal, 3–4 cores de destaque) e aplique nas variáveis `:root`. Cada material fica com a identidade da sua capa.
- **Padrões e elementos do fundo inspirados na capa** (formas, folhas, grafismos, texturas), desenhados em SVG/CSS simples. Não recorte nada da capa para usar no fundo.
- **Lombada** na cor principal da capa, com título em vertical e o ano/série num selo.
- **Primeira página**, revelada quando a capa abre: tipo do material, título, faixa colorida e subtítulo.
- **Coluna de texto:** etiqueta com o tipo, título em 3 linhas com a palavra final em degradê, faixa colorida, subtítulo, selos (ano + selos da capa) e autor(a).
- Tipografia: títulos em "Baloo 2" (ou a fonte que mais combinar com a capa) e textos em "Inter".
- Proporção do livro igual à da capa (altura ÷ largura da imagem).

## Linha do tempo da animação (manter igual ao modelo)

- 0–1,8 s: o livro entra de baixo girando e assenta; o texto aparece em sequência (etiqueta → título → faixa → subtítulo → selos → autor).
- Loop de 12 s depois da entrada:
  - pose 3/4 (rotateY −30°), com brilho passando pela capa;
  - gira para mostrar a lombada (rotateY +40°);
  - volta quase de frente e a capa abre ~68° revelando a primeira página;
  - fecha e volta à pose inicial (o último quadro do vídeo deve ser igual ao início do loop).
- Flutuação suave contínua e sombra no chão acompanhando.

## Como gravar os vídeos (mesmo método do modelo)

- Abrir a página com `?record` no Playwright/Chromium já instalado.
- Esperar `document.fonts.ready`.
- Para cada quadro (30 fps): pausar todas as animações e posicionar no tempo exato com `document.getAnimations().forEach(a => { a.pause(); a.currentTime = t })`, depois tirar um screenshot JPG de qualidade 95.
- Montar com ffmpeg: `-c:v libx264 -preset slow -crf 18 -pix_fmt yuv420p -movflags +faststart`.
- Gravar horizontal e vertical em paralelo e apagar os quadros temporários no final.

## Verificação antes de entregar

Para cada material, gere quadros de conferência (1920×1080, 1080×1920 e 390×844 de celular) nos tempos 2,5 s / 7,5 s / 10,5 s e confira:

- o texto nunca fica coberto por formas do fundo, folhas ou pela faixa do rodapé;
- a lombada e a primeira página estão legíveis;
- não há rolagem horizontal no celular;
- os dados mostrados batem com a capa.

Depois faça uma folha de contato (4 quadros de cada vídeo numa imagem só) para revisão rápida.

## Finalização

- Faça o commit de tudo na pasta `catalogo/` e envie para o branch de trabalho.
- Me envie os vídeos e uma lista com o caminho da página e dos vídeos de cada material.
- Diga claramente se algum material ficou com problema ou se faltou alguma informação.
