# Monalisa10Kids

# Monalisa 10 Kids

Site de moda infantil (0 a 12 anos) com visual minimalista e divertido: fundo preto e cores vivas (amarelo, laranja, azul, verde e rosa). O pedido é finalizado pelo **WhatsApp**, e a entrega é por **retirada na loja**.

O projeto é um **único arquivo `index.html`**, sem backend, sem build e sem instalação.

---

## Sumário

- [Páginas e funcionalidades](#páginas-e-funcionalidades)
- [Tecnologias](#tecnologias)
- [Estrutura de arquivos](#estrutura-de-arquivos)
- [Como rodar localmente](#como-rodar-localmente)
- [Como personalizar](#como-personalizar)
- [Identidade visual](#identidade-visual)
- [Como publicar](#como-publicar)
- [Checklist antes de publicar](#checklist-antes-de-publicar)
- [Limitações conhecidas](#limitações-conhecidas)

---

## Páginas e funcionalidades

A navegação é feita por hash (`#loja`, `#guia`...), então tudo acontece no mesmo arquivo, sem recarregar a página.

| Página | Endereço | O que tem |
|---|---|---|
| Início | `#home` | Hero, faixas etárias, categorias, carrossel de lançamentos, diferenciais, banner de festa, formas de pagamento, depoimentos, redes sociais e CTA final |
| Loja | `#loja` | Catálogo com filtros por faixa etária, categoria, tamanho (roupas e calçados), cor e preço, além de ordenação |
| Guia de tamanhos | `#guia` | Como medir a criança e tabelas de medidas por faixa etária |
| Quem somos | `#quem-somos` | História, valores e compromisso com o bem-estar infantil |
| Ajuda | `#ajuda` | Retirada, trocas e devoluções, privacidade (LGPD) e FAQ em acordeão |
| Contato | `#contato` | Formulário que abre o WhatsApp com a mensagem pronta, e-mail, endereço e horário |

Recursos extras:

- Botão flutuante do WhatsApp com microinteração
- Cada produto tem o botão "Pedir no WhatsApp", com o nome da peça já na mensagem
- Preço no Pix com desconto calculado automaticamente e parcelamento no cartão
- Barra de avisos animada no topo
- Layout mobile-first, totalmente responsivo
- Animações suaves ao rolar a página e efeitos de hover (respeitam `prefers-reduced-motion`)
- Acessibilidade básica: foco visível, `aria-label`, `aria-current` e `aria-pressed` nos filtros

---

## Tecnologias

- **HTML5**
- **[Tailwind CSS](https://tailwindcss.com/)** via CDN
- **JavaScript** puro (sem frameworks)
- **[Font Awesome 6](https://fontawesome.com/)** (ícones), via CDN
- **[Google Fonts](https://fonts.google.com/)**: Fredoka (títulos) e Nunito (texto)

> Tudo carrega por CDN, então é preciso **internet** para ver o site corretamente.

---

## Estrutura de arquivos

```
monalisa-10-kids/
├── index.html      # o site inteiro (HTML, CSS e JS)
├── README.md
└── img/            # (crie esta pasta) logo, foto do hero e fotos dos produtos
    ├── logo.png
    ├── hero.jpg
    └── conjunto-arco-iris.jpg
```

Dentro do `index.html`:

- `<style>`: estilos próprios (botões, cards, animações)
- `<script>` no `<head>`: configuração do Tailwind (cores e fontes)
- `<script>` no final: `CONFIG`, `PRODUCTS`, `SIZE_TABLES`, `FAQ` e toda a lógica (filtros, carrossel, menu, roteador)

---

## Como rodar localmente

### Opção 1: abrir direto

1. Salve o código como `index.html`.
2. Dê dois cliques no arquivo para abrir no navegador.

### Opção 2: VS Code com Live Server (recomendado)

1. Abra a pasta do projeto no VS Code (`File → Open Folder`).
2. Instale a extensão **Live Server** (autor: Ritwick Dey).
3. Clique com o botão direito em `index.html` e escolha **Open with Live Server**.
4. O site abre em `http://127.0.0.1:5500` e atualiza sozinho a cada `Ctrl+S`.

Para testar no celular, conecte-o ao mesmo Wi-Fi do computador e acesse o endereço de rede que o Live Server mostra.

---

## Como personalizar

Faça uma cópia de segurança do `index.html` antes de editar. No VS Code, `Ctrl+F` localiza um texto e `Ctrl+Shift+H` substitui em todo o arquivo.

### 1. Dados da loja: `CONFIG`

No final do arquivo, procure por `const CONFIG`:

```js
const CONFIG = {
  WHATSAPP: '5548999999999',          // 55 + DDD + número, só dígitos
  WHATSAPP_VIEW: '(48) 99999-9999',   // como aparece na tela
  EMAIL: 'contato@exemplo.com.br',
  CNPJ: '00.000.000/0000-00',
  ADDRESS: 'Rua Exemplo, 000 · Bairro · Cidade/UF',
  HOURS: 'Seg a Sex, 9h às 18h · Sáb, 9h às 13h',
  PIX_DISCOUNT: 5,                    // % de desconto no Pix
  INSTALLMENTS: 3,                    // parcelas no cartão
  SOCIAL: {
    instagram: 'https://www.instagram.com/SEU_PERFIL',
    tiktok: 'https://www.tiktok.com/@SEU_PERFIL',
    facebook: 'https://www.facebook.com/SEU_PERFIL'
  }
};
```

Esses valores atualizam sozinhos o cabeçalho, o rodapé, a página de contato, os cards de produto, o FAQ e todos os botões de WhatsApp.

### 2. Produtos: `PRODUCTS`

Logo abaixo do `CONFIG`. Cada linha é um produto:

```js
P(1,'Conjunto Arco-íris','conjuntos','infantil',['2','3','4','6'],['amarelo','azul'],129.9,true,'fa-shirt','img/conjunto-arco-iris.jpg'),
```

| Posição | Campo | Exemplo |
|---|---|---|
| 1 | `id` (único) | `1` |
| 2 | Nome | `'Conjunto Arco-íris'` |
| 3 | Categoria | `'conjuntos'` |
| 4 | Faixa etária | `'infantil'` |
| 5 | Tamanhos | `['2','3','4','6']` |
| 6 | Cores | `['amarelo','azul']` |
| 7 | Preço (use ponto) | `129.9` |
| 8 | É lançamento? | `true` ou `false` |
| 9 | Ícone (usado se não houver foto) | `'fa-shirt'` |
| 10 | Foto (opcional) | `'img/conjunto-arco-iris.jpg'` |

**Valores aceitos** (se escrever diferente, o filtro não encontra o produto):

- **Categoria:** `conjuntos`, `vestidos`, `pijamas`, `modapraia`, `calcados`, `acessorios`, `outlet`
- **Faixa etária:** `enxoval`, `bebe`, `infantil`, `juvenil`
- **Cor:** `amarelo`, `laranja`, `azul`, `verde`, `rosa`
- **Tamanhos de roupa:** `RN`, `P`, `M`, `G`, `1`, `2`, `3`, `4`, `6`, `8`, `10`, `12`, `U` (único)
- **Tamanhos de calçado:** `n18`, `n20`, `n22`, `n24`, `n26`, `n28`, `n30` (o `n` indica numeração)

**Dicas:**

- Para adicionar um produto, copie uma linha, use um `id` que ainda não exista e ajuste os campos.
- Produtos com `true` no campo 8 aparecem no carrossel de lançamentos da página inicial.
- Fotos funcionam melhor na proporção **4:5** (por exemplo, 800 × 1000 px), todas com o mesmo enquadramento.
- Para adicionar um tamanho, cor, categoria ou faixa etária novos, inclua-o também nas listas/objetos `SIZES`, `SHOES`, `COLORS`, `CATS` ou `AGES`.
- O filtro de preço vai até **R$ 300**. Para vender peças mais caras, troque o valor `300` no campo `#f-price` (HTML) e nos trechos `state`, `clearFilters` e `syncUI` do script.

### 3. Logo e imagens

- **Logo:** no `<header>`, procure `Troque pelo logo oficial` e substitua os três `<span>` do link por `<img src="img/logo.png" alt="Monalisa 10 Kids" class="h-10 w-auto">`. Faça o mesmo no rodapé.
- **Foto do hero:** procure `FOTO PRINCIPAL` e troque o mosaico por `<img src="img/hero.jpg" alt="..." class="w-full aspect-[4/5] rounded-[2.5rem] object-cover">`.
- **Foto de Quem somos:** procure `FOTO: loja ou equipe` e faça o mesmo.

### 4. Textos

| O que | Onde encontrar |
|---|---|
| Títulos, subtítulos e botões | No HTML, dentro de cada `<section>` |
| Depoimentos | Procure `Quem veste, ama` |
| Perguntas frequentes | `const FAQ` no script |
| Tabelas de medidas | `const SIZE_TABLES` no script |
| Políticas | Procure `Políticas e ajuda` |
| História da marca | Procure `Quem somos` |
| Título da aba e descrição no Google | `<title>` e `<meta name="description">` no topo |

### 5. Cores e fontes

As cores aparecem em três lugares: `tailwind.config` (topo), bloco `<style>` e objeto `COLORS` (script). Use `Ctrl+Shift+H` para trocar um código HEX em todo o arquivo.

Para trocar as fontes, altere o link do Google Fonts no `<head>`, o `fontFamily` no `tailwind.config` e as menções a `Fredoka` no `<style>`.

### 6. Seções e páginas

- **Remover uma seção:** apague do comentário (`<!-- DEPOIMENTOS -->`) até o `</section>` correspondente.
- **Mudar a ordem:** recorte e cole as seções dentro da página inicial.
- **Nova página:** crie `<div data-page="nome" class="hidden">`, adicione `'nome'` em `PAGES`, o título em `TITLES` e um link `<a href="#nome">` no menu.

---

## Identidade visual

| Papel | HEX |
|---|---|
| Background | `#0A0A0A` |
| Superfície (cards) | `#151515` |
| Linhas e bordas | `#262626` |
| Texto | `#FFFFFF` (principal) e `#B3B3B3` (secundário) |
| Primária (CTAs) | `#FFD23F` (amarelo) |
| Secundária | `#FF5CA8` (rosa) |
| Acentos | `#FF8A3D` (laranja), `#3DA5FF` (azul), `#3DDC84` (verde) |

Proporção sugerida: cerca de 70% preto e neutros e 30% cor. Texto escuro (`#0A0A0A`) sobre qualquer cor viva mantém bom contraste.

**Tipografia:** Fredoka (títulos, botões e logo) e Nunito (corpo do texto).

---

## Como publicar

Como é um arquivo estático, qualquer hospedagem gratuita serve:

- **[Netlify Drop](https://app.netlify.com/drop):** arraste a pasta do projeto para a página e o site fica no ar.
- **[GitHub Pages](https://pages.github.com/):** suba os arquivos para um repositório e ative o Pages em *Settings → Pages*.
- **[Vercel](https://vercel.com/):** importe o repositório ou envie a pasta.

Ao ter um domínio próprio (por exemplo, `monalisa10kids.com.br`), é possível conectá-lo em qualquer uma dessas plataformas.

---

## Checklist antes de publicar

- [ ] Preencher o `CONFIG` com WhatsApp, e-mail, CNPJ, endereço, horário e redes sociais
- [ ] Conferir o desconto do Pix e as parcelas (e se o parcelamento é sem juros)
- [ ] Substituir os **produtos de exemplo** pelos reais, com fotos
- [ ] Substituir os **depoimentos de exemplo** por relatos reais e autorizados
- [ ] Ajustar a **tabela de medidas** conforme a modelagem da loja
- [ ] Revisar os textos de **trocas, retirada e privacidade** (são modelos) com um profissional jurídico
- [ ] Escrever a **história real** da marca em "Quem somos"
- [ ] Trocar o logo em texto pelo logo oficial
- [ ] Testar os botões de WhatsApp e o formulário de contato com o número real
- [ ] Conferir o site no celular e em diferentes navegadores

---

## Limitações conhecidas

- **Sem carrinho nem checkout:** o pedido é concluído pelo WhatsApp. Se a loja quiser pagamento online, o caminho é migrar o catálogo para uma plataforma como Nuvemshop, Shopify ou Loja Integrada, mantendo este design.
- **Catálogo no código:** para alterar produtos é preciso editar o `index.html`.
- **Tailwind via CDN:** serve para protótipo e para sites pequenos. Em produção, o ideal é compilar o Tailwind para melhorar o desempenho.
- **SEO:** como as páginas são trocadas por hash dentro de um só arquivo, o Google as enxerga como uma única página. Para ranquear páginas separadas, seria necessário dividir em arquivos HTML próprios.
- **Formulário de contato:** não envia e-mail. Ele abre o WhatsApp com a mensagem já escrita.

---

## Licença e créditos

Projeto desenvolvido para **Monalisa 10 Kids**. Todos os direitos reservados à marca.

Bibliotecas de terceiros (Tailwind CSS, Font Awesome e Google Fonts) seguem suas respectivas licenças.
