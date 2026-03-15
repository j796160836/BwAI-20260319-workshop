# [Build with AI] Gemini x Antigravity 快速開發與滲透攻防實務

語言：[繁體中文](README.md) | [English](README-en.md)

## 相關資料

- [活動頁面](
https://gdg.community.dev/events/details/google-gdg-taipei-presents-build-with-ai-2026-taipei-external-5-0319-gemini-x-antigravity-kuai-su-kai-fa-yu-shen-tou-gong-fang-shi-wu/)

- [投影片](https://www.slideshare.net/slideshow/ai-gemini-x-antigravity-pentestgpt-2673/286591348)

- [工作坊筆記](
https://github.com/j796160836/BwAI-20260319-workshop)

---

# ⚠️ 免責聲明

本工作坊之核心目的在於提升參與者對 Web 應用程式漏洞的理解，進而開發更安全的軟體系統。本工作坊使用的工具僅限於「**本機**」、「**封閉範圍**」內的合法滲透測試、安全研究及合法資安防護測試之用途。

**未經授權對系統進行測試屬於違法行為。**  
**未經授權對系統進行測試屬於違法行為。**  
**未經授權對系統進行測試屬於違法行為。**  

參與者承諾遵守中華民國相關法令，包含但不限於《刑法》第 36 章「妨害電腦使用罪」（第 358 條至第 363 條）。任何超越授權範圍之行為，均可能構成非法入侵他人電腦、干擾電腦運作或製作犯罪程式等刑事責任。

*參與者於本活動結束後之任何個人行為（包含但不限於將課程技術運用於非授權環境），與本活動主辦方及講師無涉。參與者理解在實作測試過程中，可能因操作不當導致其個人電腦資料遺失或環境損毀，主辦方不負損害賠償責任。*

*請勿使用公司或個人重要的 Google 帳號進行實驗，建議申請測試用帳號，以避免因觸發平台安全機制而導致帳號停權之風險。*

---

# 工作坊內容

## 背景知識

背景知識非常重要，取決於你的認知與思考。以下是本次工作坊會接觸到的基礎技術，不需要精通，但有概念會讓你更容易上手。

### Markdown 格式

Markdown 是一種輕量級標記語言，透過簡單的純文字符號（如 `#`、`*`、`-`）即可產生結構化的文件格式。廣泛用於技術文件、GitHub README、筆記軟體等場景，學習成本極低，幾分鐘就能上手。

https://markdown.tw/

### JSON 格式

JSON（JavaScript Object Notation）是一種輕量級的資料交換格式，以 key-value 的結構組織資料。它是目前 Web API 最主流的溝通格式，前後端傳遞資料幾乎都靠它，人類可讀、機器好解析。

https://developer.mozilla.org/zh-TW/docs/Learn_web_development/Core/Scripting/JSON

### Python

Python 語法簡潔直覺，被譽為最適合入門的程式語言。從資料分析、機器學習到網頁後端開發都能勝任，擁有龐大的套件生態系，也是目前 AI 領域最主流的開發語言。

https://www.python.org/

### React

React 是由 Meta 開發的 JavaScript 前端框架，透過「元件（Component）」的概念將 UI 拆分為獨立可重用的小單元。搭配虛擬 DOM 機制實現高效渲染，是目前全球最多人使用的前端框架之一。

https://react.dev/

### CLI（命令列介面）

CLI（Command Line Interface）是透過文字指令與電腦互動的操作方式，相對於用滑鼠點擊的圖形介面（GUI）。本次工作坊會頻繁在終端機（Terminal）中輸入指令來安裝工具、啟動服務、執行測試，是開發者日常必備技能。

### Git / GitHub

Git 是目前最主流的版本控制系統，用來追蹤程式碼的修改歷史，讓你可以隨時回溯、比對、合併不同版本。GitHub 則是基於 Git 的線上平台，提供程式碼託管、協作開發與開源社群等功能。

https://git-scm.com/

### Docker / 容器 (Container)

Docker 是一種容器化技術，能將應用程式與其所有依賴（包含程式碼、函式庫、相關組態）打包封裝在一個標準單元中，確保在任何環境都能一致運行。你可以把它想像成一個輕量級的虛擬電腦（非傳統虛擬機器），啟動快、占用資源少，一致性運行。避免「在我電腦上可以跑」的問題。

https://www.docker.com/

### Nginx

Nginx 是一款高效能的網頁伺服器軟體，常用於靜態網站托管與反向代理。本次工作坊中用它來發布打包好的前端網頁，讓你可以在瀏覽器中瀏覽自己做的網站。

https://nginx.org/

### MCP（Model Context Protocol）

MCP 是一種讓 AI 模型能夠呼叫外部工具的協定，類似幫 AI 裝上「外掛」。透過 MCP，AI 不只能對話，還能實際操作工具（如掃描網站、執行指令），大幅擴展 AI 的能力範圍。

https://modelcontextprotocol.io/

### 滲透測試（Penetration Testing）

滲透測試是一種模擬駭客攻擊的安全檢測方法，目的是在壞人之前找出系統的漏洞。測試人員會以攻擊者的角度嘗試各種手法（如掃描端口、探測目錄），藉此評估系統的防禦能力並提出修補建議。本工作坊僅在本機封閉環境中進行。

https://owasp.org/www-project-web-security-testing-guide/

---

## 環境安裝

> 本工作坊需要以下工具，請依序安裝。若已安裝過可跳過該步驟。

### Antigravity

Google Antigravity（直譯：反重力）是由 Google 開發的人工智慧驅動整合式開發環境（IDE），旨在打造一個「智慧型體優先（英語：agent-first）」的軟體開發平台。

https://antigravity.google/

至官網下載對應作業系統的安裝檔：

| 作業系統 | 安裝方式 |
|---------|---------|
| macOS | 下載 `.dmg` 安裝檔 |
| Windows | 下載 `.exe` 安裝檔 |
| Linux | 下載 `.deb` 或 `.rpm` 安裝檔，或使用 `.tar.gz` |

### NodeJS

Node.js 是讓 JavaScript 可以在伺服器端執行的運行環境，也是許多前端工具鏈的基礎。

https://nodejs.org/

建議安裝 **LTS（長期支援）** 版本。

| 作業系統 | 安裝方式 |
|---------|---------|
| macOS | `brew install node` 或至官網下載 `.pkg` |
| Windows | 至官網下載 `.msi` 安裝檔（安裝時勾選 Add to PATH） |
| Linux (Ubuntu/Debian) | `sudo apt update && sudo apt install -y nodejs npm` |
| Linux (Fedora) | `sudo dnf install -y nodejs npm` |

安裝完成後驗證：

```bash
node -v
npm -v
```

### Nvm (Node Version Manager)

Nvm 可以讓你在同一台電腦上管理多個 Node.js 版本，方便切換。

https://github.com/nvm-sh/nvm

**macOS / Linux：**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

安裝完成後重新開啟終端機，即可使用：

```bash
nvm install --lts
nvm use --lts
```

**Windows：**

Windows 請改用 [nvm-windows](https://github.com/coreybutler/nvm-windows)，至 Releases 頁面下載安裝檔：

https://github.com/coreybutler/nvm-windows/releases

```powershell
nvm install lts
nvm use lts
```

### Gemini CLI

Gemini CLI 是 Google 提供的命令列 AI 助手，可在終端機中直接與 Gemini 模型互動。

https://geminicli.com/

安裝 NodeJS 之後才有 npm 可以使用，三個平台安裝指令相同：

```bash
npm install -g @google/gemini-cli
```

安裝完成後驗證：

```bash
gemini --version
```

### Docker 環境

Docker 容器是一個輕量級、可移植、自給自足的軟體運行環境，它將應用及其所有依賴封裝在一個標準單元中，實現秒級啟動與跨環境的一致性運行。

https://www.docker.com/

| 作業系統 | 安裝方式 |
|---------|---------|
| macOS | 安裝 [Docker Desktop for Mac](https://docs.docker.com/desktop/setup/install/mac-install/) |
| Windows | 安裝 [Docker Desktop for Windows](https://docs.docker.com/desktop/setup/install/windows-install/)（需啟用 WSL 2 或 Hyper-V） |
| Linux (Ubuntu/Debian) | 參考[官方文件](https://docs.docker.com/engine/install/ubuntu/)安裝 Docker Engine |

安裝完成後驗證：

```bash
docker --version
docker-compose --version
```

> **Windows 使用者注意：** Docker Desktop 需要 WSL 2 後端。若尚未啟用，請先在 PowerShell（系統管理員）執行：
>
> ```powershell
> wsl --install
> ```
>
> 重新開機後再安裝 Docker Desktop。

---

## Section 1. 用 AI Studio 來做網頁！

難度：⭐⭐

*（這部分有一些即興發揮的成分，操作步驟僅供參考，不一定會全部照原訂腳本執行）*

AI Studio
https://aistudio.google.com/

直接瀏覽網站，登入 Google 帳號即可使用。  
建議使用有兌換 Credit（抵免額）的帳號，以利後面的操作能順暢進行

### 1-1. 下 Prompt （提示詞）時間！

Prompt 就是你給 AI 的指令。

描述越具體，AI 產出的結果就越接近你要的。試著把腦袋裡的想像，化為清楚的文字描述。

#### 1-1-1. 範例一：個人網站

**❌ Bad Prompt：**

```text
#zh_tw 請幫我做一個個人網站，（...個人資料...）
```

**✅ Good Prompt：**

```text
#zh_tw 請幫我做一個個人網站，內容關於一位軟體工程師的作品集，風格為清新簡約
需要包含：
- 首頁 Hero 區塊（大標題 + 一段自我介紹）
- 作品集區塊（至少 3 個卡片，每個有圖片、標題、簡述）
- 關於我區塊（技能列表、經歷時間軸）
- 聯絡表單（姓名、Email、訊息）
- 頁尾（社群連結 icon）
配色以淡藍色與白色為主，字體使用無襯線體
```

重點：指明 **風格** 、 **必要區塊** 、 **配色與排版偏好**

#### 1-1-2. 範例二：功能型應用程式

**❌ Bad Prompt：**

```text
#zh_tw 請幫我做一個每日記帳程式，有文字框可以打
```

**✅ Good Prompt：**

```text
#zh_tw 請幫我做一個每日記帳 Web App，使用 React + TypeScript
功能需求：
- 新增一筆支出/收入（金額、分類、備註、日期）
- 分類可自訂（如：飲食、交通、娛樂、薪資）
- 首頁顯示今日花費總額與最近 10 筆紀錄
- 月報表頁面：用圓餅圖顯示各分類佔比
- 資料存在 localStorage，不需後端
- RWD 響應式設計，手機也能操作
```

重點：指明 **技術框架** 、 **功能條列式列出** 、 **資料儲存方式**

### Tips: Prompt 小技巧

- 越具體越好：與其說「做一個網站」，不如說「做一個有 3 個頁面的作品集網站」
- 善用條列式：讓 AI 更容易逐項理解你的需求
- 可以分階段下指令：先做基本架構，再逐步加功能，不用一次講完所有需求

### Tips: 個人下 Prompt 的習慣

- 使用 `#zh_tw` 開頭，強制輸出繁體中文
- 指明使用的程式語言、框架
- 功能條列式列出

### 1-2. 部署與分享

#### 1-2-1. Cloud Run 部署發佈

AI Studio 內建與 Google Cloud Run 的整合，可以一鍵將你的網頁 App 部署到網路上。

操作步驟：

1. 在 AI Studio 畫面中，點選上方的「**Publish**」按鈕
2. 系統會自動將程式碼打包並部署到 Cloud Run
3. 部署完成後會產生一組公開的 URL（如 `https://xxx.run.app`），任何人都可以透過這個網址瀏覽你的網站

> *部署會產生些微費用（運算 + 流量），但我們活動剛剛有拿到 $5 Credit 額度可使用，一般測試用量不會超過。若擔心費用，可在測試完成後至 [Google Cloud Console](https://console.cloud.google.com/) 刪除該 Cloud Run 服務。*

#### 1-2-2. 分享工作區

你可以將目前的工作區（包含你的 Prompt 和產出的程式碼）分享給其他人。

操作步驟：

1. 點選上方的「**Share**」按鈕
2. 系統會產生一組分享連結
3. 收到連結的人可以看到你的完整工作區，並按「**Remix**」以此為基礎進行二次創作

適合用來：與同學交流成果、讓別人在你的基礎上繼續開發

#### 1-2-3. 下載程式碼

如果你想把程式碼下載到本機，用自己的編輯器（如 Antigravity）繼續開發：

1. 點選上方的「**Code**」頁籤，切換到程式碼檢視模式
2. 點選右側的 **下載圖示**（Download Icon）
3. 會下載一個 `.zip` 壓縮檔，解壓縮後即可在本機開啟

#### 1-2-4. 連結 GitHub

你也可以將程式碼直接推送到 GitHub Repository，方便版本管理與後續協作。

操作步驟：

1. 點選右上角的 **齒輪圖示**（Settings）
2. 找到「**GitHub**」區塊，點選連結帳號
3. 授權 AI Studio 存取你的 GitHub
4. 建立欲推送的 Repository（選擇權限等等）

## Section 2. 用 Antigravity 來做網頁！

難度：⭐⭐⭐⭐

在 Section 1 中，我們用 AI Studio 快速生成了一個網頁。現在我們要把程式碼下載到本機，用 Antigravity 打開資料夾，繼續微調與除錯。

這個 Section 的目標是：學會用 AI IDE 搭配 Docker，在本機建立一個可運行的網站環境。

### 2-1. 用 Antigravity 開啟專案

1. 將 Section 1 下載的 `.zip` 解壓縮到你喜歡的目錄
2. 打開 Antigravity，選擇「**Open Folder**」開啟該資料夾
3. Antigravity 會自動辨識專案結構，你可以在左側看到檔案樹

### 2-2. 本機開發與除錯

這邊列出相關 React + Vite 專案常用操作指令：

```bash
# 安裝依賴
npm install

# 打開測試用伺服器
npm run dev

# 編譯檔案
npm run build
```

如果不記得可以打 `npm run` 指令即可查看指令，  
或者查看 `package.json` 查看能夠使用的指令

### 2-3. 建立本機測試環境

接下來我們要用 Docker 把網站跑起來。直接在 Antigravity 的聊天視窗輸入以下 Prompt，讓 AI 幫你生成所需的設定檔：

```text
#zh_tw 幫我寫一個 Dockerfile 與 docker-compose.yml，用 nginx 做為網站發布的容器，容器內的 80 port 對應到本機的 8080 port
```

> AI 生成的內容不一定每個人都一樣，這是正常的。  
只要最終能 `docker-compose up -d` 跑起來就好。

### 2-4. 手動補檔案（若 AI 生成有問題）

<details>
<summary>點擊展開：手動補檔案的完整內容</summary>

如果 AI 生成的檔案有錯誤或缺漏，可以手動建立以下檔案：

**.dockerignore**

```text
dist/
node_modules/
```

**Dockerfile**

```dockerfile
# Build stage
FROM node:20-alpine AS build-stage

WORKDIR /app

# Copy project files
COPY . .

# Install dependencies
RUN npm install

# Build the project
RUN npm run build

# Production stage
FROM nginx:stable-alpine AS production-stage

WORKDIR /usr/share/nginx/html

# Copy the build output from the build stage
COPY --from=build-stage /app/dist /usr/share/nginx/html

# Copy the custom nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
```

**docker-compose.yml**

```yaml
services:
  web:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "8080:80"
    restart: always
```

**nginx.conf**

```text
server {
    listen 80;
    server_name localhost;

    root /usr/share/nginx/html;

    location / {
        index index.html index.htm;
        try_files $uri $uri/ /index.html;
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
    }

    # Cache Control for static assets
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
        access_log off;
    }
}
```

</details>

### 2-5. 記得放入 `GEMINI_API_KEY`

在 AI Studio 頁面，左下角 Get API key 頁面，  
按下 `Create API key` 可以建立 API Key

https://aistudio.google.com/api-keys

將 `.env.sample` 複製一份成 `.env` 並填入 `GEMINI_API_KEY`

```text
GEMINI_API_KEY="MY_GEMINI_API_KEY"
```

### 疑難排解：我看不到網站

檢查網站的 `vite.config.ts` 根目錄是否有錯誤

```javascript
export default defineConfig(({mode}) => {
  const env = loadEnv(mode, '.', '');
  return {

    base: './',  // <-- 加上這個部分

  };
});
```

### 備註：怎麼移除 `GEMINI_API_KEY`

如果我沒用到 Gemini 的功能，怎麼移除 `GEMINI_API_KEY`？  
一樣找到 `vite.config.ts` 的檔案，  
移除 `process.env.GEMINI_API_KEY` 的段落

```javascript
export default defineConfig(({mode}) => {
  const env = loadEnv(mode, '.', '');
  return {
    // 移除這個段落
    define: {
      'process.env.GEMINI_API_KEY': JSON.stringify(env.GEMINI_API_KEY),
    },

  };
});
```

### 2-4. 容器操作

檔案都準備好之後，在專案根目錄的終端機中執行以下指令：

啟動容器（並重新編譯）：

```bash
docker compose up -d --build
```

成功後打開瀏覽器，前往 http://localhost:8080/   
即可看到你的網站。

其他常用指令：

```bash
# 關閉容器
docker compose down

# 查看 Logs（除錯時很有用）
docker compose logs

# 進入容器內部除錯（進入後可用 ls、cat 等指令檢查檔案）
docker compose exec -it web sh
```

> 每次修改程式碼後，都需要重新執行 `docker-compose up -d --build` 才會看到變更。

## Section 3. 紅隊攻擊思維：用 PentestGPT 來滲透測試

> ⚠️ 免責聲明：以下工具僅限於授權範圍內的合法滲透測試、安全研究與教育用途。未經授權對系統進行測試屬於違法行為。

難度：⭐⭐⭐⭐⭐

在前兩個 Section 中，我們用 AI 快速建立了一個網站並部署到本機。現在我們要換個角度——站在攻擊者的立場，用 AI 驅動的滲透測試工具來檢查自己的網站有沒有安全漏洞。

這就是資安領域中「紅隊（Red Team）」的概念：模擬攻擊者的行為，主動找出系統弱點，才能在真正的攻擊發生之前修補它們。

本次使用的滲透測試工具：  
https://github.com/yuhano/PentestGPT-MCP  
我修改的 image  
https://hub.docker.com/r/j796160836/pentestgpt-mcp

### 3-1. 將 PentestGPT-MCP 接上 AI 工具

PentestGPT-MCP 是一個 MCP Server，它封裝了多個滲透測試工具（如 nmap、dirb），讓 AI 可以直接呼叫這些工具進行自動化檢測。

因為安裝流程較為複雜，我這邊有修改用一個較簡單一點的方式來安裝。
我們需要把 PentestGPT-MCP 這個 MCP Server 註冊到 AI 工具中，讓 AI 能夠呼叫它。

以下提供兩種方式，擇一即可：

#### 3-1-1. 方式一：Antigravity 接上 MCP

操作步驟：

1. 點選 Antigravity 右上角的「**...**」按鈕
2. 點選「**MCP Servers**」，看到 MCP Store 畫面
3. 點選「**Manage MCP Servers**」
4. 點「**View Raw config**」，會打開設定檔 `~/.gemini/antigravity/mcp_config.json`

寫入以下 JSON（請將 `<YOUR_USER_NAME>` 替換為你的系統使用者名稱）：

**macOS / Linux / Windows 平台皆一樣：**

```json
{
  "mcpServers": {
    "pentest-tools": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "docker.io/j796160836/pentestgpt-mcp"
      ]
    }
  }
}
```

> 如有其他 mcpServers，請將新的 server 加在 `mcpServers` 物件內，以逗號分隔。

#### 3-1-2. 方式二：Gemini CLI 接上 MCP

編輯家目錄中的 `.gemini/settings.json` 檔案：

**macOS / Linux：**

```bash
vi ~/.gemini/settings.json
```

**Windows（PowerShell）：**

```powershell
notepad "$env:USERPROFILE\.gemini\settings.json"
```

在 JSON 中加入 `mcpServers` 區塊（請將 `<YOUR_USER_NAME>` 替換為你的系統使用者名稱）：

**範例：**

```json
{
  "mcpServers": {
    "pentest-tools": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "docker.io/j796160836/pentestgpt-mcp"
      ]
    }
  }
}
```

> 若檔案中已有其他設定（如 `general`、`security`），請將 `mcpServers` 加在同一層級即可，不要覆蓋既有設定。

### 3-2. 開始滲透測試

確認 Section 2 的 Docker 容器正在運行（http://localhost:8080/ 可正常瀏覽），接著在 Antigravity 或 Gemini CLI 中輸入以下 Prompt：

**範例：**

```text
#zh_tw 幫我用 pentest mcp 檢測以下這個網址有什麼問題嗎？

http://localhost:8080/
```

AI 收到指令後，會自動透過 MCP 呼叫 nmap 和 dirb 進行掃描，並回報發現的問題與建議。

### 3-3. 注意事項

- **僅限本機測試：** 路徑一定要是封閉環境的「本地 localhost」路徑，對外部網站進行未授權掃描可能違法，也有被封鎖 IP 的風險
- **dirb 字典檔路徑：** dirb 預設會去找尋 `/usr/share/wordlists/dirb/common.txt`，如果要自訂 wordlists ，請在 Prompt 中指明字典檔的實際位置
- **掃描時間：** 依字典檔大小與網站複雜度，掃描可能需要數分鐘，請耐心等待

## 補充加碼：用 Antigravity 部署到 CloudRun

### 部署到 CloudRun

操作步驟：

1. 點選 Antigravity 右上角的「**...**」按鈕
2. 點選「**MCP Servers**」，看到 MCP Store 畫面
3. 安裝 「CloudRun MCP」
4. 安裝 [gcloud cli](https://docs.cloud.google.com/sdk/docs/install-sdk)
5. 登入 Google 帳號

6. 下 Prompt

```text
#zh_tw 幫我把這程式部署到 Cloud Run
帳號名稱：xxxxx@gmail.com
專案名稱：xxxxxxxxxxx

節點用最便宜的
```

小建議：

- Prompt 一定要指明帳號名稱 與 專案名稱，  
不然他會摸索來摸索去的
- 專案請確認是否有綁定好帳單帳戶，帳單帳戶是否有餘額  
避免掉相關非技術的問題

### 刪除 CloudRun 的部署

刪除部署一樣可以下 Prompt

```text
#zh_tw 請幫我刪除 剛剛部署的網站
```

Gemini 有給你提示

> 提示：為了保持環境整潔，我建議您可以考慮手動進入 Google Cloud 控制台刪除在 gcr.io (Artifact Registry) 中產生的容器映像檔案，以免未來產生少額的存儲費用。

可以在 Google Cloud 搜尋「Artifact Registry」
https://console.cloud.google.com/artifacts

找到對應的映像檔案 (image) 將之刪除。

## 4. 結語與延伸閱讀 (Where do we go from here?)

恭喜你完成了今天的工作坊！我們從零開始，用 AI 生成了一個網頁、部署到本機環境，最後還站在攻擊者的角度檢視了自己的作品。

今天提到的一個技術，背後都是一門值得深入的學問。以下列出一些方向，供你依興趣繼續探索：

### 網頁開發

- **前端入門：** 從 HTML / CSS / JavaScript 三大基礎開始，再進入 React 等框架
- **後端入門：** 試試用 Node.js (Express) 或 Python (Flask / FastAPI) 寫一個簡單的 API
- **全端專案：** 嘗試做一個有前後端 + 資料庫的完整應用程式

### DevOps / 部署

- **Docker 進階：** 學習 multi-stage build、Docker network、volume 掛載
- **CI/CD：** 用 GitHub Actions 實現自動化測試與部署
- **雲端平台：** 深入了解 Google Cloud Run、GCP 等雲端服務

### 資安

- **OWASP Top 10：** 了解最常見的 10 種 Web 應用程式安全風險
- **CTF 練習：** 透過 [OverTheWire](https://overthewire.org/)、[Hack The Box](https://www.hackthebox.com/) 等平台練習資安技能
- **漏洞修補：** 學習如何針對 XSS、SQL Injection、CSRF 等攻擊進行防禦

### AI 輔助開發

- **Prompt Engineering：** 學習如何更有效地與 AI 溝通，提升產出品質
- **MCP 生態系：** 探索更多 MCP Server，讓 AI 能操作更多工具
- **AI Agent：** 了解 AI Agent 的概念，打造自動化的開發工作流

> 最重要的是：**動手做**。挑一個你感興趣的主題，用今天學到的方法，讓 AI 陪你一起學習與開發。

感謝參與本次工作坊，祝你在 AI 時代持續精進！🚀

---

## LICENSE

MIT