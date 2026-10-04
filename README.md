# Portfólio de Enrique Artur Rodrigues Santos

Portfólio editorial, com um prédio 3D explorável como assinatura: cada andar é uma fase da trajetória.
Feito com React, TypeScript, Vite, Tailwind CSS, three.js, React Three Fiber e drei.

- **Site editorial (página principal):** hero, projetos como case studies, sobre, trajetória e contato. Design em `src/components/portfolio/`; princípios em `CLAUDE.md`.
- **Experiência 3D (opcional):** aberta pelo botão "Explorar em 3D" ou pelo link com `#3d`. Térreo (quem sou eu), andar 01 (origem, com o quarto), elevador funcional, tour automático, HUD, sons sintetizados.
- **Português e inglês:** seletor PT | EN no cabeçalho do site, no HUD e na tela de carregamento. Troca o site inteiro na hora, inclusive as placas e telas da cena 3D; a escolha fica salva no navegador (na primeira visita, segue o idioma do navegador).
- **Fallback:** sem WebGL (ou se a cena falhar), o visitante vê um aviso e volta para o site; sem WebGL, o botão do 3D nem aparece.
- Andares 02 a 05 já existem no elevador, com placa e placeholder; os ambientes serão construídos a seguir.

## Rodar

```bash
npm install
npm run dev
```

## Controles

| Desktop | Celular / tablet |
| --- | --- |
| Clique na cena para controlar a câmera | Joystick para andar |
| WASD / setas para andar, Shift para correr | Arraste a tela para olhar |
| Mouse para olhar, roda do mouse para zoom | Toque nos objetos ou no botão INTERAGIR |
| E ou clique para interagir, ESC para fechar | Navegação por andares na lateral |
| Dentro do elevador: teclas 0–5 | |

## Onde mexer

| O quê | Arquivo |
| --- | --- |
| Nome, cargo, links de contato | `src/data/profile.ts` |
| Textos do site (hero, sobre, ferramentas, trajetória) | `src/data/about.ts` |
| Andares (título, texto, iluminação, áreas) | `src/data/floors.ts` |
| Textos dos objetos interativos | `src/data/interactions.ts` |
| Projetos (case studies do site e futuras salas do andar 04) | `src/data/projects.ts` |
| Capturas dos projetos | `public/images/` + campo `images` em `projects.ts` (sem imagem, aparece a ilustração de `portfolio/mockups.tsx`) |
| Roteiro do "Explorar automaticamente" | `src/data/tour.ts` |
| Modelos 3D externos (.glb) | `src/data/models.ts` e `public/models/` |
| Textos da interface e do site | nos próprios componentes, como `t({ pt: "...", en: "..." })` |
| Currículo em português / inglês | `public/curriculo.html` / `public/resume.html` |

### Traduções

Todo texto visível é escrito nos dois idiomas, lado a lado: `{ pt: "Origem", en: "Origin" }` (tipo `Localized`, em `src/lib/i18n/language.ts`). Nos componentes, use `const t = useT()` e `t({ pt, en })`; fora do React (desenhos em canvas, tour), use `t(...)` importado do mesmo arquivo. Texturas criadas com `useCanvasTexture` são redesenhadas sozinhas quando o idioma muda.

### Adicionar um objeto interativo

1. Crie a entrada em `src/data/interactions.ts` (`id`, `title`, `category`, `interactionType`, `description`; textos em `{ pt, en }`).
2. Envolva o objeto 3D na sala:

```tsx
<InteractiveObject id="certificado" position={[1, 1.5, -4.9]} reaction="hop">
  <mesh>{/* geometria e material do objeto */}</mesh>
</InteractiveObject>
```

Tipos de interação: `modal` (painel lateral), `screen` (computador simulado), `tooltip` (cartão que some sozinho) e `reaction` (só reage, com legenda curta opcional).

### Construir um andar

Crie o componente em `src/components/3d/Floors/`, registre em `FLOOR_COMPONENTS` (`Floors/FloorContent.tsx`) e mude o `status` do andar para `"ready"` em `floors.ts`.

## Estrutura

```
src/
  app/            App (escolhe site, 3D ou fallback) e ErrorBoundary
  components/
    3d/           Building, Floors, Rooms, InteractiveObject, Elevator, Camera, Lighting
    portfolio/    site editorial (página principal) e ilustrações das interfaces dos projetos
    site/         Reveal (animação de entrada)
  data/           conteúdo: perfil, andares, interações, projetos, tour, modelos
  lib/            interaction, performance, accessibility, audio, input, physics, store
  ui/             HUD, Modal, FloorNavigation, LoadingScreen, TouchControls, Fallback
public/
  curriculo.html  currículo para imprimir / salvar em PDF
  resume.html     o mesmo currículo, em inglês
  models/         modelos .glb opcionais
```

## Desempenho

- O three.js fica num chunk separado, baixado só quando o visitante abre o prédio; o site não carrega nada de 3D.
- Qualidade automática por dispositivo (alta, média, baixa), com ajuste de resolução pelo FPS e o botão **Modo desempenho** (sem sombras, menos luzes, resolução menor).
- Só o andar atual tem interior, luzes e colisões; os outros andares são uma casca leve com janelas iluminadas.
- Livros e prédios da cidade usam instancing; texturas de placas e telas são desenhadas em canvas (sem downloads).

## Publicar no GitHub Pages

1. `npm run build`
2. Envie o **conteúdo** de `dist/` para o repositório `seuusuario.github.io` (branch `main`).
3. Settings → Pages → Deploy from a branch.

Substitua os placeholders de e-mail, GitHub e LinkedIn em `src/data/profile.ts`, `src/data/projects.ts`, `public/curriculo.html` e `public/resume.html` antes de publicar.
