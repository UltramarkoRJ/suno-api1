<div align="center">
  <h1 align="center"">
      Suno AI API
  </h1>
  <p>用 API 调用 suno.ai 的音乐生成 AI，并且可以轻松集成到 GPTs 等 agent 中。</p>
  <p>👉 我们更新很快，欢迎 star。</p>
</div>
<p align="center">
  <a target="_blank" href="./README.md">English</a> 
  | <a target="_blank" href="./README_CN.md">简体中文</a> 
  | <a target="_blank" href="./README_PT.md">Português</a>
  | <a target="_blank" href="https://suno.gcui.ai">Demo</a> 
  | <a target="_blank" href="https://suno.gcui.ai/docs">文档</a> 
  | <a target="_blank" href="https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fgcui-art%2Fsuno-api&env=SUNO_COOKIE&project-name=suno-api&repository-name=suno-api">一键部署到 Vercel</a> 
  
</p>
<p align="center">
  <a href="https://www.producthunt.com/products/gcui-art-suno-api-open-source-sunoai-api/reviews?utm_source=badge-product_review&utm_medium=badge&utm_souce=badge-gcui&#0045;art&#0045;suno&#0045;api&#0045;open&#0045;source&#0045;sunoai&#0045;api" target="_blank"><img src="https://api.producthunt.com/widgets/embed-image/v1/product_review.svg?product_id=577408&theme=light" alt="gcui&#0045;art&#0047;suno&#0045;api&#0058;Open&#0045;source&#0032;SunoAI&#0032;API - Use&#0032;API&#0032;to&#0032;call&#0032;the&#0032;music&#0032;generation&#0032;AI&#0032;of&#0032;suno&#0046;ai&#0046; | Product Hunt" style="width: 250px; height: 54px;" width="250" height="54" /></a>
</p>
> 🔥 我们新的开源项目: [Album AI - 用自然语言与你的图库对话!](https://github.com/gcui-art/album-ai)

![suno-api banner](https://github.com/gcui-art/suno-api/blob/main/public/suno-banner.png)

## 简介

Suno.ai v3 是一个令人惊叹的 AI 音乐服务，虽然官方还没有开放 API，但我们已经迫不及待的想在某些地方集成它的能力。
我们发现有一些用户也有类似需求，于是我们将这个项目开源了，希望你们喜欢。

## Demo

我们部署了一个示例，绑定了一个免费的 suno 账号，所以它每天有使用限制，但你可以看到它运行起来的样子：
[suno.gcui.ai](https://suno.gcui.ai)

## Features

- 完美的实现了 app.suno.ai 中的大部分 API
- 自动保持账号活跃
- 兼容 OpenAI 的 `/v1/chat/completions` API 格式
- 支持 Custom Mode
- 一键部署到 vercel
- 除了标准 API，还适配了 GPTs、coze 等 Agent 平台的 API Schema，所以你可以把它当做一个 LLM 的工具/插件/Action，集成到任意 AI Agent 中。
- 宽松的开源协议，你可以随意的集成和修改。

## 如何开始使用？

### 1. 获取你的 app.suno.ai 账号的 cookie

1. 浏览器访问 [app.suno.ai](https://app.suno.ai)
2. 打开浏览器的控制台：按下 `F12` 或者`开发者工具`
3. 选择`网络`标签
4. 刷新页面
5. 找到包含`client?_clerk_js_version`关键词的请求
6. 点击并切换到 `Header` 标签
7. 找到 `Cookie` 部分，鼠标复制 Cookie 的值

![获取cookie](https://github.com/gcui-art/suno-api/blob/main/public/get-cookie-demo.gif)

### 2. 克隆并部署本项目

你可以选择自己喜欢的部署方式：

#### 部署到 Vercel

[![部署到 Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fgcui-art%2Fsuno-api&env=SUNO_COOKIE&project-name=suno-api&repository-name=suno-api)

#### 本地运行

```bash
git clone https://github.com/gcui-art/suno-api.git
cd suno-api
npm install
```

或者，你也可以使用 [Docker Compose](https://docs.docker.com/compose/)

```bash
docker compose build && docker compose up
```

### 3. 配置 suno-api

- 如果部署到了 Vercel，请在 Vercel 后台，添加环境变量 `SUNO_COOKIE`，值为第一步获取的 cookie。
- 如果在本地运行，请在 .env 文件中添加：

```bash
SUNO_COOKIE=<your-cookie>
```

### 4. 运行 suno api

- 如果部署到了 Vercel：
  - 请在 Vercel 后台，点击 `Deploy`，等待部署成功。
  - 访问 `https://<vercel分配的域名>/api/get_limit` API 进行测试
- 如果在本地运行：
  - 请运行 `npm run dev`
  - 访问 `http://localhost:3000/api/get_limit` API 进行测试
- 如果返回以下结果：

```json
{
  "credits_left": 0,
  "period": "string",
  "monthly_limit": 0,
  "monthly_usage": 0
}
```

则已经正常运行。

### 5. 使用 Suno API

你可以在 [suno.gcui.ai](https://suno.gcui.ai/docs)查看详细的 API 文档，并在线测试。

## API 说明

Suno API 目前主要实现了以下 API:

```bash
- `/api/generate`: 创建音乐
- `/v1/chat/completions`: 创建音乐 - 用OpenAI API 兼容的格式调用 generate API
- `/api/custom_generate`: 创建音乐（自定义模式，支持设置歌词、音乐风格、设置标题等）
- `/api/generate_lyrics`: 根据Prompt创建歌词
- `/api/get`: 根据id获取音乐信息。获取多个请用","分隔，不传ids则返回所有音乐
- `/api/get_limit`: 获取配额信息
- `/api/extend_audio`: 在一首音乐的基础上，扩展音乐长度
- `/api/clip`: 检索特定音乐的信息
- `/api/concat`: 合并音乐，将扩展后的音乐和原始音乐合并
```

详细文档请查看演示站点:
[suno.gcui.ai/docs](https://suno.gcui.ai/docs)

## API 集成代码示例

### Python

```python
import time
import requests

# replace your vercel domain
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


if __name__ == '__main__':
    data = generate_audio_by_prompt({
        "prompt": "A popular heavy metal song about war, sung by a deep-voiced male singer, slowly and melodiously. The lyrics depict the sorrow of people after the war.",
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

// replace your vercel domain
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

async function main() {
  const data = await generateAudioByPrompt({
    prompt:
      "A popular heavy metal song about war, sung by a deep-voiced male singer, slowly and melodiously. The lyrics depict the sorrow of people after the war.",
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

## 集成到到常见的自定义 Agent 中

你可以把 suno ai 当做一个 工具/插件/Action 集成到你的 AI Agent 中。

### 集成到 GPTs

您可以通定义自定义操作（Actions）将此 Suno API 与 OpenAI 的 GPTs 集成。
1.  在配置您的 GPT 时，选择“创建新操作” (Create new action)。
2.  选择“导入 OpenAPI schema” (Import OpenAPI schema)。
3.  提供指向您部署的 Suno API 实例中的 `public/swagger-suno-api.json` 文件的 URL (例如, `https://your-deployed-domain.vercel.app/swagger-suno-api.json`)。或者，您可以复制并粘贴 `swagger-suno-api.json` 文件的内容。
4.  可用的 API 端点将被自动检测到。在 GPT 编辑器中根据需要配置它们。
5.  您还需要配置身份验证。此 API 使用 cookie (`SUNO_COOKIE`) 进行身份验证，需要作为标头发送。您可能需要在 GPT Actions 设置中设置身份验证方案（如 API Key），其中 "API Key" 实际上是您的 Suno 会话 cookie。指导用户以这种方式提供他们的 cookie。

### 集成到 Coze

要将 Suno API 与 Coze (或其他类似的机器人平台) 集成：
1.  这些平台通常允许通过指定 API 端点来添加自定义工具或插件。
2.  您可以定义一个新插件并手动添加此 Suno API 实例提供的每个 API 端点 (例如, `/api/generate`, `/api/custom_generate` 等)。
3.  有关如何添加用于身份验证的请求标头的具体信息，请参阅您的 Coze 文档。您需要将 `SUNO_COOKIE` 作为标头传递。
4.  或者，如果 Coze 支持导入 OpenAPI schema，您或许可以使用 `public/swagger-suno-api.json` 文件。

### 集成到 LangChain

要将此 Suno API 与 LangChain 一起使用，您通常会创建一个自定义 `Tool`。
1.  定义一个继承自 LangChain 的 `BaseTool` 的新类。
2.  在此类中，实现 `_run` 方法 (以及可选的 `_arun` 用于异步操作)。
3.  此方法将向所需的 Suno API 端点发出 HTTP 请求 (例如, 使用像 `requests` 或 `aiohttp` 这样的库)。
4.  确保在请求标头中包含 `SUNO_COOKIE` 以进行身份验证。
5.  然后，您可以实例化此工具并将其包含在 LangChain agent 的工具列表中。

概念示例:
```python
from langchain_core.tools import BaseTool
import requests
import os

class SunoMusicTool(BaseTool):
    name = "SunoMusicGenerator"
    description = "根据提示使用 Suno API 生成音乐，或执行其他与音乐相关的任务。"
    # 如果需要结构化输入，请定义 args_schema

    def _run(self, prompt: str, mode: str = "generate", **kwargs): # 根据需要添加其他参数
        base_url = os.environ.get("SUNO_API_BASE_URL")
        suno_cookie = os.environ.get("SUNO_COOKIE")
        headers = {"Cookie": f"COOKIE={suno_cookie}"} # 如果您的部署期望不同的 cookie 标头名称，请进行调整

        if mode == "generate":
            response = requests.post(f"{base_url}/api/generate", json={"prompt": prompt, **kwargs}, headers=headers)
        elif mode == "custom_generate":
            response = requests.post(f"{base_url}/api/custom_generate", json={"prompt": prompt, **kwargs}, headers=headers)
        # 为其他 API 端点（如 get, extend_audio 等）添加其他模式
        else:
            return "无效模式。"

        response.raise_for_status() # 对错误的状态码抛出异常
        return response.json()

    async def _arun(self, query: str):
        # 如果需要，实现异步版本
        raise NotImplementedError("SunoMusicTool 尚不支持异步")

# 用法:
# tool = SunoMusicTool()
# result = tool.run(prompt="史诗般的太空战斗音乐", make_instrumental=True, wait_audio=True)
```
这是一个简化示例。您需要更稳健地处理 API 基础 URL、cookie 管理 (可能通过环境变量或配置) 和错误处理。有关有效负载结构的更多详细信息，请参阅 `API 集成代码示例` 部分。

## 贡献指南

您有四种方式支持本项目：

1. Fork 项目并提交 PR：我们欢迎任何让这个组件和Editor变的更好的PR。
2. 提交Issue：我们欢迎任何合理的建议、bug反馈。
3. 捐赠：在项目的顶部我们放置了 Sponsor 按钮，如果这个项目帮助到了您，你可以请我们喝一杯，干杯☕。
4. 推荐：向其他人推荐本项目；点击Star；使用本项目后放置外链。

## 许可证

LGPL-3.0 或更高版本

## 你有一个问题/建议/困难/Bug？

我们使用Github的Issue来管理这些反馈，你可以提交一个。我们会经常来处理。

## 相关链接

- 项目仓库: [github.com/gcui-art/suno-api](https://github.com/gcui-art/suno-api)
- Suno.ai 官网: [suno.ai](https://suno.ai)
- 演示站点: [suno.gcui.ai](https://suno.gcui.ai)

## 声明

suno-api 是一个非官方的开源项目，仅供学习和研究使用。
