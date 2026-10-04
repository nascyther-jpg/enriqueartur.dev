# Portfólio de Enrique Artur

## Design principles

Este projeto é um portfólio profissional de desenvolvedor.

Prioridades:

1. Design autoral
2. Hierarquia visual
3. Tipografia
4. Espaçamento
5. Usabilidade
6. Performance
7. Acessibilidade
8. Animação

NUNCA adicionar um componente apenas porque ele parece bonito.

Evitar:
- gradientes excessivos
- glassmorphism
- neon
- partículas
- blobs
- excesso de cards
- efeitos de glow
- animações desnecessárias
- aparência de landing page gerada por IA

Componentes do Spectrum UI (ou Aceternity, Magic UI, shadcn/ui) só entram se melhorarem a experiência,
e sempre customizados para o design do projeto.

Antes de finalizar uma alteração visual:
1. execute o projeto
2. abra com Playwright
3. teste desktop
4. teste mobile
5. verifique overflow
6. verifique navegação
7. analise hierarquia visual
8. corrija problemas encontrados

O objetivo é que o resultado pareça um produto desenvolvido por um designer + desenvolvedor experiente,
e não um template gerado automaticamente.

## Convenções

- Todo texto visível existe em português e inglês, lado a lado: `{ pt: "...", en: "..." }`
  (`src/lib/i18n/language.ts`). Nada de string de interface sem as duas versões.
- Tokens de cor e tipografia ficam em `src/index.css` (`--color-paper`, `--color-ink`, ...). Não usar cores soltas
  nos componentes do site.
- O site editorial é a página principal; o prédio 3D é uma assinatura opcional (botão "Explorar em 3D" ou `#3d` na URL).
