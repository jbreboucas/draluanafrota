# Link da bio — Dra. Luana Frota

Página única (mobile-first, estilo Linktree) para o link da bio do Instagram, com:
- Botão principal que abre um **chat simulando o WhatsApp**, com um bot que qualifica o lead (nome, idade, área de interesse, urgência) antes de mandar para o WhatsApp comercial.
- **Meta Pixel** (ID `28111047135225241`) instalado, com eventos de conversão prontos para campanhas do Meta Ads.
- Galeria de antes/depois, FAQ, links para Instagram e localização.

## 1. Colocar as fotos reais

As imagens que você mandou ainda **não estão nos arquivos** (recebi só em anexo no chat, não como arquivo no seu computador). A página já está pronta para recebê-las — hoje ela mostra um placeholder cinza/dourado no lugar de cada foto que falta.

Salve os arquivos dentro de `assets/img/` **exatamente com estes nomes**:

| Nome do arquivo | Onde aparece | Sugestão de qual foto usar |
|---|---|---|
| `profile.jpg` | Foto de perfil circular (topo da página e cabeçalho do chat) | O print de perfil do Instagram ou uma foto de rosto próxima |
| `antes-depois-1.jpg` | Galeria — harmonização facial frontal | Foto frontal (acne → pele lisa) |
| `antes-depois-2.jpg` | Galeria — harmonização facial perfil | Foto de perfil (acne → pele lisa) |
| `antes-depois-3.jpg` | Galeria — preenchimento labial | Foto de boca em diagonal |
| `antes-depois-4.jpg` | Galeria — preenchimento labial perfil | Foto de perfil com pescoço esticado |
| `logo.png` | Usada como imagem de compartilhamento (Open Graph) | A logo "Luana Frota" |

Se algum arquivo não existir, a página automaticamente mostra o placeholder — nada quebra, só fica menos bonito até você trocar.

## 2. Publicar no GitHub Pages

```bash
cd draluanafrota-linkbio
git init
git add .
git commit -m "Landing page do link da bio"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
git push -u origin main
```

Depois, no GitHub: **Settings → Pages → Branch: main → pasta `/ (root)`** → salvar.
Sua página fica em `https://SEU-USUARIO.github.io/SEU-REPOSITORIO/`.

Coloque esse link no campo "Site" da bio do Instagram (@draluanafrota).

## 3. Como funciona o rastreamento (Meta Ads)

O Pixel `28111047135225241` já está no `<head>`. Eventos disparados:

| Evento | Quando dispara | Uso no Meta Ads |
|---|---|---|
| `PageView` | Ao abrir a página | Padrão, alcance/visitas |
| `InitiateCheckout` | Ao abrir o chat de qualificação | Sinal de interesse (topo de funil) |
| `CompleteRegistration` | Ao terminar as 3 perguntas do bot | Lead qualificado que respondeu tudo |
| `Lead` | Ao clicar em "Enviar para o WhatsApp" (fluxo completo OU "prefiro falar direto") | **Evento de conversão principal** — use este para otimizar as campanhas |
| `ClickInstagram` / `ClickMaps` / `ChatAbandoned` (customizados) | Cliques secundários e abandono do chat | Análise de funil, não usar como otimização |

Para conferir se está disparando certo depois do deploy: **Gerenciador de Eventos → Testar Eventos**, cole a URL da página publicada e clique nos botões.

Se quiser rastrear a origem exata da campanha, adicione parâmetros na URL do anúncio, ex:
`https://SEU-USUARIO.github.io/SEU-REPOSITORIO/?utm_campaign=labios_agosto&utm_source=meta`
A página já lê esses parâmetros e inclui a campanha na mensagem enviada ao WhatsApp.

## 4. Configurações que você pode trocar

Tudo no topo do `<script>` no final do `index.html`:

```js
var WHATSAPP_NUMBER = "5585988310834"; // número comercial que recebe os leads
var INSTAGRAM_URL = "https://www.instagram.com/draluanafrota/";
var MAPS_URL = "..."; // link do Google Maps
```

## 5. Testar localmente antes de subir

```bash
cd draluanafrota-linkbio
python3 -m http.server 8000
```
Abra `http://localhost:8000` no navegador do celular (ou no modo mobile do Chrome DevTools).
