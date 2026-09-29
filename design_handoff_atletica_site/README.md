# Handoff: Site one-page — Atlética Academia Feminina

## Overview
Site institucional one-page (+ página de Galeria) para a **Atlética Academia Feminina**, academia exclusivamente feminina na Rua Santa Bárbara, 206 – Centro, Santa Bárbara d'Oeste – SP, CEP 13450-010. Objetivo: apresentar a academia com estética "futurística, tecnológica e humanizada" (dark mode, glassmorphism, animações guiadas por scroll e mouse, inspiradas no estilo de sites da Apple) e converter visitantes via WhatsApp.

## About the Design Files
Os arquivos deste pacote são **referências de design feitas em HTML** — protótipos que mostram aparência e comportamento pretendidos, **não código de produção para copiar diretamente**. A tarefa é **recriar estes designs no ambiente do codebase alvo** (React/Next, Vue, Astro etc.) usando seus padrões. Se ainda não existe codebase, recomenda-se **Next.js ou Astro + Tailwind** (o briefing original pediu HTML5 semântico, Tailwind e JS vanilla modular), com as animações implementadas via `requestAnimationFrame` + `transform/opacity` (ou GSAP ScrollTrigger / Framer Motion, se preferir).

Os `.dc.html` abrem direto no navegador (dependem de `support.js`, incluso). O markup está em `<x-dc>…</x-dc>` e a lógica em `<script type="text/x-dc" data-dc-script>` (classe `Component`, estilo React class component: `state`, `setState`, `componentDidMount`, `renderVals()` devolve os valores usados nos `{{ holes }}` do template).

## Fidelity
**High-fidelity.** Cores, tipografia, espaçamentos, textos e interações são finais — recriar com fidelidade. Exceções marcadas como **PENDENTE** abaixo.

---

## Screens / Views

### 1. Página principal — `Athletic Academia v2.dc.html`
Container de conteúdo: `max-width:1240px; margin:0 auto; padding: 0 24px`. Fundo raiz: `radial-gradient(1200px 700px at 85% -10%, rgba(94,26,60,.55), transparent 60%), radial-gradient(900px 600px at -10% 40%, rgba(94,26,60,.3), transparent 60%), #0A0A0C`. Root com `overflow-x: clip` (não `hidden`, para não quebrar `position: sticky`).

Ordem das seções:

**A. Header fixo (glass)**
- `position:fixed; top:16px; centered; width:min(1240px, calc(100% - 32px)); border-radius:18px; background:rgba(18,18,21,.6); backdrop-filter:blur(16px); border:1px solid rgba(255,255,255,.08); padding:10px 12px 10px 20px; z-index:50`.
- Esquerda: logo (`assets/logo-mark.png`, 30px de altura) + "ATLÉTICA" (Syne 700, 15px, letter-spacing .08em; oculto abaixo de 420px).
- Nav (desktop ≥1000px): Sobre (#sobre), Modalidades, Aulas, Planos, Galeria (abre a página Galeria com transição). Outfit 14px, #B9B2B7 → hover #fff, gap 26px.
- CTA "MATRICULE-SE JÁ": #FF2A6D, branco, 600 13px, radius 12px, min-height 44px, animação `athPulse` (box-shadow magenta pulsando 2.6s). Abre WhatsApp com mensagem pré-preenchida (ver Links).
- Mobile (<1000px): botão ☰ 44×44 abre um painel dropdown (glass, top 88px) com os mesmos links.

**B. Hero (sticky, 190vh de altura)**
- Inner `position:sticky; top:0; height:100svh`. Conteúdo centralizado em coluna: logo (clamp 40–96px, 7vh), tag "★ Espaço Exclusivo Para Você, Mulher" (pill, cor #E0A96D, borda rgba(224,169,109,.35), bg rgba(224,169,109,.08)), H1 "TRANSFORME SUA **MELHOR** VERSÃO" ("MELHOR" em #FF2A6D) em Syne 800, `font-size:min(8.4cqw, 9vh)` dentro de um container com `container-type:inline-size`, line-height .95, letter-spacing -.02em. Subtítulo Outfit clamp(16–19px) #B9B2B7 max 560px. Dois CTAs pill (radius 999): "Agende sua Aula Experimental →" (magenta, efeito magnético) e "Conhecer Planos e Benefícios" (outline com brilho radial que segue o cursor).
- Espaçamentos verticais em `clamp(…, vh, …)` para caber em telas baixas (540px) sem sobrepor o header.
- Hint "ROLE PARA DESCOBRIR ↓" (11px, .24em) — oculto se innerHeight < 760.
- **Animações:** título revela letra por letra no load (cada letra: opacity 0→1, translateY(.6em) rotate(6deg) blur(6px) → none; 700ms, delay 200 + i·35ms, cubic-bezier(.2,.8,.2,1)). Parallax do mouse: logo translate(mx·40, my·40) rotate(mx·10°), título translate(-mx·16, -my·10). Scroll: conteúdo faz fade-out + translateY(-90px) + scale(.88) de p=.15 a p=1 da seção.

**C. Manifesto "Sobre" (#sobre, sticky, 240vh)**
- Label mono "SOBRE A ATLÉTICA" + parágrafo grande em Syne 700 clamp(28px, 4.3vw, 62px): "Mais do que um lugar para treinar, um ambiente acolhedor onde cada aluna conta com acompanhamento próximo de professoras preparadas para orientar execuções, ajustar equipamentos e garantir segurança e eficiência."
- Cada palavra começa em opacity .14 e acende até 1 conforme o progresso de scroll (`opacity = .14 + .86·clamp(p·1.2·N − i)`). Palavras destacadas em magenta: acolhedor, acompanhamento, próximo, segurança, eficiência.

**D. 01 — Diferenciais (#diferenciais)**
- H2: "O que faz a diferença no seu treino." + quebra + "Seja Atlética Feminina." (#FF2A6D).
- Grid auto-fit minmax(300px,1fr), gap 18px, 3 cards glass (radius 24, padding 34/30, min-height 280, brilho radial seguindo o mouse via CSS vars --mx/--my):
  1. Acompanhamento Estratégico — "Professoras presentes em cada série para garantir propósito, correção e evolução constante." (accent #FF2A6D)
  2. Bioimpedância Avançada — "Acompanhamento preciso da composição corporal para metas reais." (#05D9E8)
  3. Comunidade & Conexão — "Eventos exclusivos, como as aulas de Pilates com Vinho e o Arraiá da Atlética, que unem leveza, saúde e momentos entre mulheres." (#E0A96D)

**E. 02 — Estrutura Completa (#estrutura) + anel LPF**
- Grid 2 colunas `5fr / 7fr` (1 coluna < 860px), gap 48.
- **Esquerda sticky (top 110px):** label "02 — ESTRUTURA & SEGURANÇA", H2 "Estrutura Completa", e abaixo o **anel LPF**: bloco quadrado `width:min(100%, 46vh, 340px)`, SVG com círculo base (stroke rgba(255,255,255,.08)) e círculo de progresso (#FF2A6D, stroke-width 1.2, dasharray 295.3, rotate -90). Dentro: "LPF – LOW PRESSURE FITNESS" (mono 10px #05D9E8), "até", número grande (Syne 800 min(72px,11vh)) + "cm" magenta, texto "de redução na circunferência abdominal com o sistema de treinamento postural e respiratório focado no fortalecimento do core." (12px).
- **Comportamento:** enquanto a coluna direita rola, o anel preenche e o contador sobe 0→12, `t = clamp((0.25·H − rect.top) / (rect.height − 0.6·H))`.
- **Direita:** 4 itens (border-top, padding 38px 0). Cada um: número colorido, H3 Syne clamp(26–44px), texto 17px #B9B2B7. Opacidade/translateX conforme distância ao centro da viewport (.18 → 1, 24px → 0).
  1. Localização privilegiada — Acesso rápido e estacionamento simplificado.
  2. Segurança garantida — Suporte dedicado no período noturno (das 18h até o encerramento das atividades).
  3. Espaços amplos e climatizados — Salas modernas e climatizadas, incluindo um espaço exclusivo para RPM e duas salas integradas para ginástica.
  4. Comodidade e Bem-estar — Estúdio de Pilates completo, sala dedicada para avaliação funcional e vestiários espaçosos.

**F. 03 — Modalidades (#modalidades, galeria horizontal sticky)**
- Sticky 100svh; o scroll vertical traduz uma trilha horizontal (`translateX(-p·(track.scrollWidth − innerWidth))`). A altura da seção é calculada em JS: `innerHeight + dist + 0.3·innerHeight`, recalculada quando a largura da trilha muda (troca de aba/resize).
- Cabeçalho: label, H2 "11 modalidades. / Escolha como você quer se mover." (clamp 26–46px), **abas** (pills 40px: Todas 11 · Aeróbica 4 · Cardio 5 · Resistência 6 · Dança 2; ativa = bg/borda #FF2A6D) e barra de progresso (2px, magenta, scaleX(p)).
- Cards: `width:min(76vw,330px); height:min(48vh,460px); radius 24; tilt 3D no mouse` (rotateY/rotateX ±7°, scale 1.02, borda vira rgba(255,42,109,.45)). Foto full-bleed `object-fit:cover`, gradiente escuro embaixo, número em chip, tag opcional (pill #E0A96D), título Syne 25px, descrição 15px.
- **Exceção Balance Pilates:** layout "split" — foto no topo (`flex:1 0 56%`, object-position 55% 60%), tag e número sobre a foto, texto abaixo em fundo sólido #121215 (título 22px, descrição com line-clamp 2). Feito porque a frase cobria a aluna.
- Ao trocar de aba, cards entram com stagger (opacity/translateY 30px/scale .96, 600ms, 60ms entre cards).
- Modalidades (categoria → foto):
  | # | Modalidade | Tag | Categorias | Foto |
  |---|---|---|---|---|
  | 01 | Musculação Personalizada | – | res | mod/musculacao.jpg |
  | 02 | LPF – Low Pressure Fitness | – | res | mod/lpf.jpg |
  | 03 | Balance Pilates & Estúdio | FLOW & WINE | res | mod/pilates.jpg (split) |
  | 04 | FitDance | – | dan, aer | mod/fitdance.jpg |
  | 05 | Zumba | – | dan, aer | mod/danca.jpg |
  | 06 | Spinning / RPM | – | car | mod/spinning.jpg |
  | 07 | HIIT | 30 MIN | car, res | mod/hiit.jpg |
  | 08 | Jump | – | aer, car | mod/jump.jpg |
  | 09 | Treinamento Funcional | – | res, car | mod/funcional.jpg |
  | 10 | Yoga | – | res | mod/yoga.jpg |
  | 11 | Treino de Corrida | EXTERNO | car, aer | mod/corrida.jpg |
  Textos exatos de cada card estão no array `mods` dentro de `allMods()` no arquivo.

**G. 04 — Grade de Aulas (#aulas)**
- Grid `2fr / 1fr` (1 coluna < 860px). Esquerda: seletor Seg–Sáb (botões flex:1, ativo magenta), faixa "FUNCIONAMENTO · {DIA}" com horário real, lista de aulas (hora Syne 20px, nome, local, ponto colorido). Nota: "Horários ilustrativos — confirme a grade atual pelo WhatsApp."
- Horários de funcionamento (reais): Seg–Qui 05:30–11:00 | 13:30–20:30 · Sex 05:30–11:00 | 13:30–19:30 · Sáb 07:00–11:00.
- Direita: "AVISOS DA ROTINA" — acordeão de 3 itens (um aberto por vez): Inverno: aqueça sempre / Treino e ciclo menstrual / Pós-fim de semana, sem neura.
- **PENDENTE:** a lista de aulas por dia é ilustrativa — substituir pela grade real.

**H. Avaliações (#avaliacoes)** — `max-width:1000px`
- H2 "O que nossas alunas dizem de nós." (clamp 30–46px). Selo à direita: G oficial do Google (img gstatic 28px em quadrado branco 48px radius 14), "4.7 de 5", 5 estrelas #FBBC05 com a 5ª parcialmente preenchida (94%), "Avaliações no Google".
- Carrossel: card glass (radius 24, padding clamp(22–36px), gradientes radiais magenta/teal, aspas gigantes ao fundo), avatar "C" (gradiente #FF2A6D→#5E1A3C), nome **"Cliente Google"** em todas, ★★★★★ + "via [G]", texto Syne 600 clamp(17–22px). Barra de tempo no rodapé do card (gradiente magenta→teal).
- Auto-avanço a cada **5s**; pausa no hover; setas SVG chevron (círculo 52px desktop ao lado do card; 44px abaixo no mobile < 700px). Sem dots. Transição: texto entra com translateX(±40px) + blur(6px) → 0, 650ms.
- 20 depoimentos no array `reviews`.
- **PENDENTE / IMPORTANTE:** os 20 textos foram escritos como exemplo. **Não publicar como avaliações reais do Google** — substituir pelos textos verdadeiros do perfil no Google, e confirmar a nota 4.7.

**I. 05 — Planos (#planos)**
- 3 cards (Essencial / Completo — badge "MAIS ESCOLHIDO", borda magenta / Bem-estar — borda rosé). Lista de benefícios com ✓ teal. Botão "Consultar valores no WhatsApp" com mensagem específica por plano.
- **PENDENTE:** nomes, preços e benefícios são exemplos — aguardando dados reais.

**J. Nossa História (#historia)** — perto do fim da página, por pedido do cliente
- Grid `6fr / 5fr` (1 coluna < 860px): foto da fachada (`assets/fachada.jpg`, aspect 4/3, radius 28, object-position 62%; scale .92→1 ao entrar + parallax interno) | texto: label "CONHEÇA A NOSSA TRAJETÓRIA", H2 "Nossa História", "DESDE 06.11.2010" (#E0A96D), 2 parágrafos (texto do cliente, verbatim no arquivo).
- Abaixo: 2 cards "Nossa Equipe" e "Equipamentos de Ponta" (texto verbatim).
- Abaixo: **card de entrada da Galeria** — link grande (borda magenta, brilho no mouse): "GALERIA · 21 FOTOS", "Conheça nosso espaço", "Musculação, cardio, salas de aula, estúdio de Pilates e vestiários.", botão "Ver galeria →", mosaico de 3 fotos (00, 17, 13).

**K. 06 — Contato (#contato)**
- Card com endereço + CEP, telefones (19) 3626-7606 / (19) 97418-3482 (WhatsApp), e-mail contato@atleticaacademia.com.br, #eusouatletica, links YouTube e Instagram (ícones oficiais), botão "Falar no WhatsApp". Mapa Google embed com filtro dark `invert(.92) hue-rotate(180deg) saturate(.6) contrast(.9)`.

**L. Footer**
- Logo + "ATLÉTICA ACADEMIA FEMININA" + #eusouatletica. **Links concentrados** em 3 botões (64px, radius 18, hover sobe 3px e borda magenta): Instagram (ícone oficial, gradiente IG), YouTube (▶ em #FF0033), WhatsApp (ícone oficial em #25D366). Linha inferior: endereço + "Copyright © 2026 Atlética Academia Feminina. Todos os direitos reservados."

### 2. Galeria — `Galeria.dc.html`
- Header glass: "← Voltar ao site" (outline), logo, "AGENDAR VISITA" (magenta → WhatsApp).
- H1 "Conheça nosso espaço." (Syne 800 clamp 40–84px), subtítulo, abas: Todos 21 · Musculação 7 · Cardio & RPM 3 · Salas de aula 5 · Estúdio de Pilates 4 · Vestiários 2.
- Grid masonry-like: `repeat(auto-fill, minmax(280px,1fr))`, `grid-auto-rows:clamp(180px,20vw,240px)`, `grid-auto-flow:dense`, gap 14; algumas fotos ocupam 2×2 (só na aba Todos e > 640px). Hover: zoom 1.06, borda magenta. Chip com categoria.
- Lightbox: fundo rgba(6,6,8,.92) blur, imagem contida, setas ←/→, ✕, teclado (Esc/←/→), contador "Categoria · n / total".
- Mapeamento foto→categoria no array `photos` (índices 00–20 em `assets/galeria/`).

---

## Interactions & Behavior
- **Transição entre páginas (Galeria):** ao clicar em qualquer link de Galeria, um overlay fixo (`radial-gradient(#FF2A6D, #5E1A3C 55%, #0A0A0C)`) expande em `clip-path: circle(0%→150% at clickX clickY)` (800ms, cubic-bezier(.7,0,.2,1)); a posição é salva em `sessionStorage.athTransition`; a Galeria abre com o círculo contraindo a partir do mesmo ponto (900ms) e o conteúdo entra em stagger. "Voltar ao site" faz o inverso (`sessionStorage.athBack`). Tratar `pageshow` (bfcache) para cancelar o overlay.
- **Scroll reveal genérico** (`data-reveal`): IntersectionObserver threshold .12 → opacity 0→1, translateY(50px) scale(.96) → none, 900ms.
- **Brilho no cursor:** círculo fixo 640px `radial-gradient(rgba(255,42,109,.13), transparent 62%)`, mix-blend screen, segue o mouse com lerp .12; desligado em `(hover: none)`.
- **Glow em cards/botões:** `onMouseMove` define `--mx/--my` no elemento; background `radial-gradient(… at var(--mx) var(--my), rgba(255,42,109,.12–.2), …)`.
- **Botão magnético:** translate((x−cx)·.25, (y−cy)·.35), volta ao sair; transition .25s.
- Todas as animações contínuas num único loop rAF; só `transform`, `opacity`, `clip-path`, `stroke-dashoffset`.
- **Responsivo:** breakpoints usados — 420px (esconde texto do logo, CTA mais estreito), 700px (setas do carrossel vão para baixo), 860px (grids de 2 colunas viram 1), 1000px (nav → menu hambúrguer). Seções sticky usam `100svh`. Alvos de toque ≥ 44px. Testado sem overflow horizontal em 336px.

## State Management
- Principal: `day` (0–5, grade), `openNotice` (acordeão), `menuOpen`, `cat` (aba de modalidades: all/aer/car/res/dan), `rev` (índice do carrossel), `w` (largura da janela p/ breakpoints). Refs internas: timer do carrossel (`_revT`, pausa no hover e quando a aba do navegador está oculta), `galDist`.
- Galeria: `cat`, `lb` (índice do lightbox, -1 fechado).
- Sem fetch de dados; tudo estático.

## Links (WhatsApp com mensagem pré-preenchida)
Base: `https://wa.me/5519974183482?text=<encodeURIComponent(msg)>` (o link curto `wa.me/message/7NTMKZEYCBS2J1` não aceita texto pré-preenchido).
- MATRICULE-SE JÁ: "Olá! Gostaria de saber mais informações sobre a matrícula na Atlética Academia."
- Aula experimental: "Olá! Gostaria de agendar uma aula experimental na Atlética Academia. Quais horários estão disponíveis?"
- Planos: "Olá! Quero saber a respeito dos valores do plano {Essencial|Completo|Bem-estar} da Atlética Academia."
- Contato/rodapé: "Olá! Vim pelo site da Atlética Academia e gostaria de mais informações."
- Galeria (Agendar visita): "Olá! Vi a galeria do site e gostaria de agendar uma visita à Atlética Academia."
- Instagram: https://www.instagram.com/atleticaacademia/
- YouTube: https://www.youtube.com/channel/UCOxSuXTsIbVq-jPDJtkiYBQ

## Design Tokens
**Cores**
- Fundo: #0A0A0C (primário), #121215 (superfície sólida), wine #5E1A3C (gradientes de fundo), #1f0f18 / #2a0f1e (fundos de card)
- Glass: rgba(255,255,255,.03) + `backdrop-filter: blur(16px)`, borda rgba(255,255,255,.08–.14)
- Texto: #F4F1F3 (principal), #D9D3D7, #B9B2B7 (secundário), #8a8087 (terciário/labels), #6f676c (rodapé)
- Magenta (primária/CTA): #FF2A6D (hover de link #ff6b96)
- Teal (detalhes técnicos): #05D9E8
- Ouro rosé (exclusividade/bem-estar): #E0A96D
- Estrelas: #FBBC05. Marcas: WhatsApp #25D366, YouTube #FF0033, gradiente oficial do Instagram.

**Tipografia** (Google Fonts)
- Títulos: **Syne** 600/700/800 — H1 min(8.4cqw, 9vh); H2 clamp(34px, 4.5vw, 58px), lh 1.02, ls -.02em; H3 24–26px.
- Corpo: **Outfit** 300–600 — 15–18px, lh 1.5–1.7.
- Labels: ui-monospace/Menlo 12px, ls .14em, uppercase, geralmente #FF2A6D.

**Raios:** 999 (pills), 28 (mídias grandes), 24 (cards), 18–20 (cards menores/header), 12–14 (botões).
**Espaçamento:** seções 80–100px verticais; gaps 14/18/24/40/48/56.
**Sombras:** CTA `0 10px 40px -10px rgba(255,42,109,.7)`; card de avaliação `0 30px 80px -30px rgba(0,0,0,.6)`; logo `drop-shadow(0 16px 40px rgba(255,42,109,.45))`.
**Easing padrão:** cubic-bezier(.2,.8,.2,1); transições de página cubic-bezier(.7,0,.2,1).

## Assets
- `assets/logo-mark.png` — símbolo "a" do logo do cliente, extraído do arquivo original (fundo removido, branco transparente).
- `assets/mod/*.jpg` — 11 fotos das modalidades (fornecidas pelo cliente; imagens geradas por IA — algumas mostram a marca "FEMME" nas roupas/paredes; **recomenda-se trocar por fotos reais da academia** quando possível).
- `assets/fachada.jpg` — fachada da academia (fornecida pelo cliente).
- `assets/galeria/00–20.jpg` — 21 fotos reais do espaço (redimensionadas p/ 1200px).
- Ícone Google: `https://www.gstatic.com/images/branding/product/2x/googleg_48dp.png` (hospedar localmente em produção).
- Ícones Instagram/WhatsApp: paths SVG oficiais (Simple Icons), inline no arquivo.

## Pendências do cliente
1. Grade real de aulas por dia.
2. Planos reais (nomes, valores, benefícios).
3. Textos reais das avaliações do Google (+ confirmar nota 4.7).
4. Idealmente, fotos reais para os cards de modalidades.

## Files
- `Athletic Academia v2.dc.html` — página principal (versão atual).
- `Galeria.dc.html` — página da galeria.
- `support.js` — runtime necessário para abrir os `.dc.html` no navegador.
- `assets/` — todas as imagens.
