<div align="center">
  <h1 align="center">
      API Suno AI
  </h1>
  <p>Use a API para chamar a IA de geração de música do Suno.ai e integre-a facilmente em agentes como GPTs.</p>
  <p>👉 Atualizamos rapidamente, por favor, marque com estrela.</p>
</div>
<p align="center">
  <a target="_blank" href="./README.md">English</a>
  | <a target="_blank" href="./README_CN.md">简体中文</a>
  | <a target="_blank" href="./README_PT.md">Português</a>
  | <a target="_blank" href="https://suno.gcui.ai">Demonstração</a>
  | <a target="_blank" href="https://suno.gcui.ai/docs">Documentação</a>
  | <a target="_blank" href="https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fgcui-art%2Fsuno-api&env=SUNO_COOKIE&project-name=suno-api&repository-name=suno-api">Implantar com Vercel</a>
</p>
<p align="center">
  <a href="https://www.producthunt.com/products/gcui-art-suno-api-open-source-sunoai-api/reviews?utm_source=badge-product_review&utm_medium=badge&utm_souce=badge-gcui&#0045;art&#0045;suno&#0045;api&#0045;open&#0045;source&#0045;sunoai&#0045;api" target="_blank"><img src="https://api.producthunt.com/widgets/embed-image/v1/product_review.svg?product_id=577408&theme=light" alt="gcui&#0045;art&#0047;suno&#0045;api&#0058;Open&#0045;source&#0032;SunoAI&#0032;API - Use&#0032;API&#0032;to&#0032;call&#0032;the&#0032;music&#0032;generation&#0032;AI&#0032;of&#0032;suno&#0046;ai&#0046; | Product Hunt" style="width: 250px; height: 54px;" width="250" height="54" /></a>
</p>

> 🔥 Confira nosso novo projeto de código aberto: [Album AI - Converse com sua galeria usando linguagem simples!](https://github.com/gcui-art/album-ai)

![suno-api banner](https://github.com/gcui-art/suno-api/blob/main/public/suno-banner.png)

## Introdução

Suno.ai v3 é um incrível serviço de música com IA. Embora a API oficial ainda não esteja disponível, mal podíamos esperar para integrar suas capacidades em algum lugar.

Descobrimos que alguns usuários têm necessidades semelhantes, então decidimos abrir o código deste projeto, esperando que você goste.

## Demonstração

Implantamos um exemplo vinculado a uma conta gratuita do Suno, portanto, ele tem limites de uso diário, mas você pode ver como funciona:
[suno.gcui.ai](https://suno.gcui.ai)

## Funcionalidades

- Implementa perfeitamente a API de criação do app.suno.ai
- Mantém automaticamente a conta ativa.
- Compatível com o formato da API `/v1/chat/completions` da OpenAI.
- Suporta Modo Personalizado
- Implantação com um clique no Vercel
- Além da API padrão, também se adapta ao Esquema de API de plataformas de Agentes como GPTs e Coze, para que você possa usá-lo como uma ferramenta/plugin/Ação para LLMs e integrá-lo a qualquer Agente de IA.
- Licença de código aberto permissiva, permitindo que você integre e modifique livremente.

## Começando

### 1. Obtenha o cookie da sua conta app.suno.ai

1. Acesse [app.suno.ai](https://app.suno.ai) usando seu navegador.
2. Abra o console do navegador: pressione `F12` ou acesse as `Ferramentas do Desenvolvedor`.
3. Navegue até a aba `Rede`.
4. Atualize a página rapidamente.
5. Identifique a solicitação que inclui a palavra-chave `client?_clerk_js_version`.
6. Clique nela e mude para a aba `Cabeçalho`.
7. Localize a seção `Cookie`, passe o mouse sobre ela e copie o valor do Cookie.

![get cookie](https://github.com/gcui-art/suno-api/blob/main/public/get-cookie-demo.gif)

### 2. Clone e implante este projeto

Você pode escolher seu método de implantação preferido:

#### Implantar no Vercel

[![Implantar com Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fgcui-art%2Fsuno-api&env=SUNO_COOKIE&project-name=suno-api&repository-name=suno-api)

#### Executar localmente

```bash
git clone https://github.com/gcui-art/suno-api.git
cd suno-api
npm install
```

Alternativamente, você pode usar o [Docker Compose](https://docs.docker.com/compose/)

```bash
docker compose build && docker compose up
```

### 3. Configure o suno-api

- Se implantado no Vercel, adicione uma variável de ambiente `SUNO_COOKIE` no painel do Vercel, com o valor do cookie obtido na primeira etapa.

- Se você estiver executando localmente, certifique-se de adicionar o seguinte ao seu arquivo `.env`:

```bash
SUNO_COOKIE=<seu-cookie>
```

### 4. Execute o suno api

- Se você implantou no Vercel:
  - Clique em Implantar no painel do Vercel e aguarde a implantação ser bem-sucedida.
  - Visite a API `https://<dominio-atribuido-pelo-vercel>/api/get_limit` para testar.
- Se estiver executando localmente:
  - Execute `npm run dev`.
  - Visite a API `http://localhost:3000/api/get_limit` para testar.
- Se o seguinte resultado for retornado:

```json
{
  "credits_left": 50,
  "period": "day",
  "monthly_limit": 50,
  "monthly_usage": 50
}
```

isso significa que o programa está funcionando normally.

### 5. Use a API Suno

Você pode conferir a documentação detalhada da API em:
[suno.gcui.ai/docs](https://suno.gcui.ai/docs)

## Referência da API

A API Suno atualmente implementa principalmente as seguintes APIs:

```bash
- `/api/generate`: Gerar música
- `/v1/chat/completions`: Gerar música - Chame a API de geração em um formato que funcione com a API da OpenAI.
- `/api/custom_generate`: Gerar música (Modo Personalizado, suporta configuração de letras, estilo musical, título, etc.)
- `/api/generate_lyrics`: Gerar letras com base no prompt
- `/api/get`: Obter informações da música com base no id. Use “,” para separar vários ids.
    Se nenhum ID for fornecido, todas as músicas serão retornadas.
- `/api/get_limit`: Obter informações da cota
- `/api/extend_audio`: Estender a duração do áudio
- `/api/clip`: Obter informações do clipe com base no ID passado como parâmetro de consulta `id`
- `/api/concat`: Gerar a música inteira a partir de extensões
```

Para documentação mais detalhada, confira o site de demonstração:
[suno.gcui.ai/docs](https://suno.gcui.ai/docs)

## Exemplo de Código de Integração da API

### Python

```python
import time
import requests

# substitua seu domínio vercel
base_url = 'http://localhost:3000'


def custom_generate_audio(payload):
    url = f"{base_url}/api/custom_generate"
    response = requests.post(url, json=payload, headers={'Content-Type': 'application/json'})
    return response.json()


def extend_audio(payload):
    url = f"{base_url}/api/extend_audio"
    response = requests.post(url, json=payload, headers={'Content-Type': 'application/json'})
    return response.json()

def generate_audio_by_prompt(payload):
    url = f"{base_url}/api/generate"
    response = requests.post(url, json=payload, headers={'Content-Type': 'application/json'})
    return response.json()


def get_audio_information(audio_ids):
    url = f"{base_url}/api/get?ids={audio_ids}"
    response = requests.get(url)
    return response.json()


def get_quota_information():
    url = f"{base_url}/api/get_limit"
    response = requests.get(url)
    return response.json()

def get_clip(clip_id):
    url = f"{base_url}/api/clip?id={clip_id}"
    response = requests.get(url)
    return response.json()

def generate_whole_song(clip_id):
    payloyd = {"clip_id": clip_id}
    url = f"{base_url}/api/concat"
    response = requests.post(url, json=payload)
    return response.json()


if __name__ == '__main__':
    data = generate_audio_by_prompt({
        "prompt": "Uma música popular de heavy metal sobre a guerra, cantada por um cantor masculino de voz profunda, lenta e melodiosamente. A letra retrata a tristeza das pessoas após a guerra.",
        "make_instrumental": False,
        "wait_audio": False
    })

    ids = f"{data[0]['id']},{data[1]['id']}"
    print(f"ids: {ids}")

    for _ in range(60):
        data = get_audio_information(ids)
        if data[0]["status"] == 'streaming':
            print(f"{data[0]['id']} ==> {data[0]['audio_url']}")
            print(f"{data[1]['id']} ==> {data[1]['audio_url']}")
            break
        # sleep 5s
        time.sleep(5)

```

### Js

```js
const axios = require("axios");

// substitua seu domínio vercel
const baseUrl = "http://localhost:3000";

async function customGenerateAudio(payload) {
  const url = `${baseUrl}/api/custom_generate`;
  const response = await axios.post(url, payload, {
    headers: { "Content-Type": "application/json" },
  });
  return response.data;
}

async function generateAudioByPrompt(payload) {
  const url = `${baseUrl}/api/generate`;
  const response = await axios.post(url, payload, {
    headers: { "Content-Type": "application/json" },
  });
  return response.data;
}

async function extendAudio(payload) {
  const url = `${baseUrl}/api/extend_audio`;
  const response = await axios.post(url, payload, {
    headers: { "Content-Type": "application/json" },
  });
  return response.data;
}

async function getAudioInformation(audioIds) {
  const url = `${baseUrl}/api/get?ids=${audioIds}`;
  const response = await axios.get(url);
  return response.data;
}

async function getQuotaInformation() {
  const url = `${baseUrl}/api/get_limit`;
  const response = await axios.get(url);
  return response.data;
}

async function getClipInformation(clipId) {
  const url = `${baseUrl}/api/clip?id=${clipId}`;
  const response = await axios.get(url);
  return response.data;
}

async function main() {
  const data = await generateAudioByPrompt({
    prompt:
      "Uma música popular de heavy metal sobre a guerra, cantada por um cantor masculino de voz profunda, lenta e melodiosamente. A letra retrata a tristeza das pessoas após a guerra.",
    make_instrumental: false,
    wait_audio: false,
  });

  const ids = `${data[0].id},${data[1].id}`;
  console.log(`ids: ${ids}`);

  for (let i = 0; i < 60; i++) {
    const data = await getAudioInformation(ids);
    if (data[0].status === "streaming") {
      console.log(`${data[0].id} ==> ${data[0].audio_url}`);
      console.log(`${data[1].id} ==> ${data[1].audio_url}`);
      break;
    }
    // sleep 5s
    await new Promise((resolve) => setTimeout(resolve, 5000));
  }
}

main();
```

## Integração com Agentes Personalizados

Você pode integrar o Suno AI como uma ferramenta/plugin/ação em seu agente de IA.

### Integração com GPTs

Você pode integrar esta API Suno com os GPTs da OpenAI definindo Ações personalizadas.
1.  Ao configurar seu GPT, selecione "Criar nova ação".
2.  Escolha "Importar esquema OpenAPI".
3.  Forneça a URL para o arquivo `public/swagger-suno-api.json` da sua instância da API Suno implantada (por exemplo, `https://seu-dominio-implantado.vercel.app/swagger-suno-api.json`). Alternativamente, você pode copiar e colar o conteúdo do arquivo `swagger-suno-api.json`.
4.  Os endpoints da API disponíveis serão detectados automaticamente. Configure-os conforme necessário no editor GPT.
5.  Você também precisará configurar a autenticação. Esta API usa um cookie (`SUNO_COOKIE`) para autenticação, que precisa ser enviado como um cabeçalho. Pode ser necessário configurar um esquema de autenticação (como Chave de API) nas configurações das Ações GPT, onde a "Chave de API" é, na verdade, seu cookie de sessão Suno. Instrua os usuários a fornecerem seus cookies desta forma.

### Integração com Coze

Para integrar a API Suno com o Coze (ou outras plataformas de bot semelhantes):
1.  Essas plataformas geralmente permitem adicionar ferramentas ou plugins personalizados especificando endpoints de API.
2.  Você pode definir um novo plugin e adicionar manualmente cada endpoint da API fornecido por esta instância da API Suno (por exemplo, `/api/generate`, `/api/custom_generate`, etc.).
3.  Consulte a documentação do Coze para obter detalhes sobre como adicionar cabeçalhos de solicitação para autenticação. Você precisará passar o `SUNO_COOKIE` como um cabeçalho.
4.  Alternativamente, se o Coze suportar a importação de esquemas OpenAPI, você poderá usar o arquivo `public/swagger-suno-api.json`.

### Integração com LangChain

Para usar esta API Suno com LangChain, você normalmente criaria uma `Tool` personalizada.
1.  Defina uma nova classe que herda de `BaseTool` do LangChain.
2.  Nesta classe, implemente o método `_run` (e opcionalmente `_arun` para operações assíncronas).
3.  Este método fará requisições HTTP para os endpoints desejados da API Suno (por exemplo, usando uma biblioteca como `requests` ou `aiohttp`).
4.  Certifique-se de incluir o `SUNO_COOKIE` nos cabeçalhos da requisição para autenticação.
5.  Você pode então instanciar esta ferramenta e incluí-la na lista de ferramentas do seu agente LangChain.

Conceito de exemplo:
```python
from langchain_core.tools import BaseTool
import requests
import os

class SunoMusicTool(BaseTool):
    name = "SunoMusicGenerator"
    description = "Gera música usando a API Suno com base em um prompt ou executa outras tarefas relacionadas à música."
    # Defina o esquema de args se desejar entrada estruturada

    def _run(self, prompt: str, mode: str = "generate", **kwargs): # Adicione outros parâmetros conforme necessário
        base_url = os.environ.get("SUNO_API_BASE_URL")
        suno_cookie = os.environ.get("SUNO_COOKIE")
        headers = {"Cookie": f"COOKIE={suno_cookie}"} # Ajuste se sua implantação esperar um nome de cabeçalho de cookie diferente

        if mode == "generate":
            response = requests.post(f"{base_url}/api/generate", json={"prompt": prompt, **kwargs}, headers=headers)
        elif mode == "custom_generate":
            response = requests.post(f"{base_url}/api/custom_generate", json={"prompt": prompt, **kwargs}, headers=headers)
        # Adicione outros modos para outros endpoints da API como get, extend_audio etc.
        else:
            return "Modo inválido."

        response.raise_for_status() # Lança uma exceção para códigos de status ruins
        return response.json()

    async def _arun(self, query: str):
        # Implemente a versão assíncrona se necessário
        raise NotImplementedError("SunoMusicTool ainda não suporta async")

# Uso:
# tool = SunoMusicTool()
# result = tool.run(prompt="Música épica de batalha espacial", make_instrumental=True, wait_audio=True)
```
Este é um exemplo simplificado. Você precisaria lidar com URLs base da API, gerenciamento de cookies (talvez por meio de variáveis de ambiente ou configuração) e tratamento de erros de forma mais robusta. Consulte a seção `Exemplo de Código de Integração da API` para mais detalhes sobre as estruturas de payload.

## Contribuindo

Existem quatro maneiras de apoiar este projeto:

1. Fork e Envie Pull Requests: Agradecemos quaisquer PRs que melhorem o componente ou editor.
2. Abra Issues: Agradecemos sugestões razoáveis e relatórios de bugs.
3. Doe: Se este projeto o ajudou, considere nos pagar um café usando o botão Patrocinar no topo do projeto. Saúde! ☕
4. Divulgue: Recomende este projeto a outras pessoas, marque o repositório com estrela ou adicione um backlink após usar o projeto.

## Perguntas, Sugestões, Problemas ou Bugs?

Usamos GitHub Issues para gerenciar feedback. Sinta-se à vontade para abrir uma issue e nós a resolveremos prontamente.

## Licença

LGPL-3.0 ou posterior

## Links Relacionados

- Repositório do projeto: [github.com/gcui-art/suno-api](https://github.com/gcui-art/suno-api)
- Site oficial do Suno.ai: [suno.ai](https://suno.ai)
- Demonstração: [suno.gcui.ai](https://suno.gcui.ai)
- Album AI: [Gere metadados de imagem automaticamente e converse com o álbum. RAG + Álbum.](https://github.com/gcui-art/album-ai)

## Declaração

suno-api é um projeto de código aberto não oficial, destinado apenas para fins de aprendizado e pesquisa.
