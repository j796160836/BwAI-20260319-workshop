# [Build with AI] Gemini x Antigravity — Rapid Development & Penetration Testing Workshop

Language：[繁體中文](README.md) | [English](README-en.md)

## Related Content

- [Event page](
https://gdg.community.dev/events/details/google-gdg-taipei-presents-build-with-ai-2026-taipei-external-5-0319-gemini-x-antigravity-kuai-su-kai-fa-yu-shen-tou-gong-fang-shi-wu/)

- [Slides](https://www.slideshare.net/slideshow/ai-gemini-x-antigravity-pentestgpt-2673/286591348)

- [Workshop notes](https://github.com/j796160836/BwAI-20260319-workshop)

---

# ⚠️ Disclaimer

The core purpose of this workshop is to enhance participants' understanding of web application vulnerabilities, thereby developing more secure software systems. The tools used in this workshop are strictly limited to legitimate penetration testing, security research, and authorized security defense testing within a **local** and **closed** environment.

**Unauthorized testing of systems is illegal.**
**Unauthorized testing of systems is illegal.**
**Unauthorized testing of systems is illegal.**

Participants agree to comply with all applicable laws of the Republic of China (Taiwan), including but not limited to Chapter 36 of the Criminal Code — "Offenses Against Computer Usage" (Articles 358–363). Any actions exceeding authorized scope may constitute criminal liability, including unauthorized access to computer systems, interference with computer operations, or creation of criminal programs.

*Any personal actions taken by participants after the event (including but not limited to applying workshop techniques in unauthorized environments) are unrelated to the event organizers and instructors. Participants understand that during hands-on exercises, improper operations may result in personal data loss or environment damage; the organizers bear no liability for such damages.*

*Please do not use your company or personal primary Google account for experiments. It is recommended to create a test account to avoid the risk of account suspension due to triggering platform security mechanisms.*

---

# Workshop Content

## Background Knowledge

Background knowledge is crucial and depends on your awareness and critical thinking. Below are the foundational technologies covered in this workshop. You don't need to master them, but having a basic understanding will make it much easier to follow along.

### Markdown

Markdown is a lightweight markup language that uses simple plain-text symbols (such as `#`, `*`, `-`) to produce structured document formats. It is widely used in technical documentation, GitHub READMEs, note-taking apps, and more. The learning curve is extremely low — you can get started in just a few minutes.

https://markdown.tw/

### JSON

JSON (JavaScript Object Notation) is a lightweight data interchange format that organizes data in key-value structures. It is currently the most mainstream communication format for Web APIs — nearly all frontend-backend data transfer relies on it. It's human-readable and easy for machines to parse.

https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON

### Python

Python has concise and intuitive syntax, and is often regarded as the best programming language for beginners. It can handle everything from data analysis and machine learning to web backend development. With a vast package ecosystem, it is also the most mainstream development language in the AI field.

https://www.python.org/

### React

React is a JavaScript frontend framework developed by Meta that uses the concept of "Components" to break down the UI into independent, reusable units. Combined with its virtual DOM mechanism for efficient rendering, it is one of the most widely used frontend frameworks in the world.

https://react.dev/

### CLI (Command Line Interface)

CLI (Command Line Interface) is a way of interacting with a computer through text commands, as opposed to clicking with a mouse in a graphical user interface (GUI). This workshop frequently involves typing commands in the terminal to install tools, start services, and run tests — an essential skill for developers.

### Git / GitHub

Git is currently the most mainstream version control system, used to track the modification history of code, allowing you to revert, compare, and merge different versions at any time. GitHub is an online platform built on Git that provides code hosting, collaborative development, and open-source community features.

https://git-scm.com/

### Docker / Containers

Docker is a containerization technology that packages an application along with all its dependencies (including code, libraries, and configurations) into a standardized unit, ensuring consistent execution across any environment. Think of it as a lightweight virtual computer (not a traditional virtual machine) — fast to start, low on resource usage, and consistent in execution. It eliminates the "it works on my machine" problem.

https://www.docker.com/

### Nginx

Nginx is a high-performance web server software commonly used for static site hosting and reverse proxying. In this workshop, we use it to serve the packaged frontend pages, allowing you to browse your own website in a browser.

https://nginx.org/

### MCP (Model Context Protocol)

MCP is a protocol that enables AI models to call external tools — similar to installing "plugins" for AI. Through MCP, AI can not only have conversations but also operate tools (such as scanning websites or executing commands), greatly expanding the AI's capabilities.

https://modelcontextprotocol.io/

### Penetration Testing

Penetration testing is a security assessment method that simulates hacker attacks, aiming to find system vulnerabilities before malicious actors do. Testers adopt an attacker's perspective and try various techniques (such as port scanning and directory probing) to evaluate the system's defenses and provide remediation recommendations. This workshop is conducted exclusively in a local, closed environment.

https://owasp.org/www-project-web-security-testing-guide/

---

## Environment Setup

> This workshop requires the following tools. Please install them in order. If you've already installed any of them, you can skip that step.

### Antigravity

Google Antigravity is an AI-powered integrated development environment (IDE) developed by Google, designed to create an "agent-first" software development platform.

https://antigravity.google/

Download the installer for your operating system from the official website:

| OS | Installation |
|----|-------------|
| macOS | Download the `.dmg` installer |
| Windows | Download the `.exe` installer |
| Linux | Download the `.deb` or `.rpm` installer, or use `.tar.gz` |

### Node.js

Node.js is a runtime environment that allows JavaScript to run on the server side, and is the foundation of many frontend toolchains.

https://nodejs.org/

It is recommended to install the **LTS (Long-Term Support)** version.

| OS | Installation |
|----|-------------|
| macOS | `brew install node` or download `.pkg` from the official website |
| Windows | Download the `.msi` installer from the official website (check "Add to PATH" during installation) |
| Linux (Ubuntu/Debian) | `sudo apt update && sudo apt install -y nodejs npm` |
| Linux (Fedora) | `sudo dnf install -y nodejs npm` |

Verify installation:

```bash
node -v
npm -v
```

### nvm (Node Version Manager)

nvm allows you to manage multiple Node.js versions on the same computer, making it easy to switch between them.

https://github.com/nvm-sh/nvm

**macOS / Linux:**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

After installation, reopen your terminal and use:

```bash
nvm install --lts
nvm use --lts
```

**Windows:**

For Windows, use [nvm-windows](https://github.com/coreybutler/nvm-windows). Download the installer from the Releases page:

https://github.com/coreybutler/nvm-windows/releases

```powershell
nvm install lts
nvm use lts
```

### Gemini CLI

Gemini CLI is a command-line AI assistant provided by Google that allows you to interact with Gemini models directly in the terminal.

https://geminicli.com/

After installing Node.js, you'll have npm available. The installation command is the same across all platforms:

```bash
npm install -g @google/gemini-cli
```

Verify installation:

```bash
gemini --version
```

### Docker Environment

A Docker container is a lightweight, portable, self-sufficient software runtime environment that packages an application and all its dependencies into a standardized unit, enabling instant startup and consistent execution across environments.

https://www.docker.com/

| OS | Installation |
|----|-------------|
| macOS | Install [Docker Desktop for Mac](https://docs.docker.com/desktop/setup/install/mac-install/) |
| Windows | Install [Docker Desktop for Windows](https://docs.docker.com/desktop/setup/install/windows-install/) (requires WSL 2 or Hyper-V) |
| Linux (Ubuntu/Debian) | Follow the [official documentation](https://docs.docker.com/engine/install/ubuntu/) to install Docker Engine |

Verify installation:

```bash
docker --version
docker-compose --version
```

> **Windows users note:** Docker Desktop requires the WSL 2 backend. If not yet enabled, run the following in PowerShell (as Administrator):
>
> ```powershell
> wsl --install
> ```
>
> Restart your computer, then install Docker Desktop.

---

## Section 1. Build a Website with AI Studio!

Difficulty: ⭐⭐

*(This section has some improvisation involved. The steps below are for reference only and may not all be followed exactly as scripted.)*

AI Studio
https://aistudio.google.com/

Simply visit the website and log in with your Google account to get started.
It is recommended to use an account with redeemed Credits to ensure smooth operation later.

### 1-1. Prompt Time!

A prompt is the instruction you give to the AI.

The more specific your description, the closer the AI's output will be to what you want. Try to turn the ideas in your head into clear, written descriptions.

#### 1-1-1. Example 1: Personal Website

**❌ Bad Prompt:**

```text
Please make me a personal website, (...personal info...)
```

**✅ Good Prompt:**

```text
Please make me a personal website about a software engineer's portfolio,
with a clean and minimalist style.
It should include:
- A Hero section on the homepage (large heading + self-introduction)
- A portfolio section (at least 3 cards, each with an image, title, and description)
- An About Me section (skill list, experience timeline)
- A contact form (name, email, message)
- A footer (social media link icons)
Color scheme: primarily light blue and white, using sans-serif fonts
```

Key point: Specify the **style**, **required sections**, and **color/layout preferences**

#### 1-1-2. Example 2: Functional Application

**❌ Bad Prompt:**

```text
Please make me a daily expense tracker, with a text box to type in
```

**✅ Good Prompt:**

```text
Please make me a daily expense tracking Web App using React + TypeScript
Feature requirements:
- Add an expense/income entry (amount, category, notes, date)
- Customizable categories (e.g., food, transportation, entertainment, salary)
- Homepage displays today's total spending and the 10 most recent entries
- Monthly report page: pie chart showing category proportions
- Data stored in localStorage, no backend needed
- Responsive design (RWD), mobile-friendly
```

Key point: Specify the **tech stack**, **list features itemized**, and **data storage method**

### Tips: Prompt Techniques

- The more specific, the better: Instead of "make a website," say "make a portfolio website with 3 pages"
- Use bullet points: Makes it easier for AI to understand your requirements item by item
- Give instructions in stages: Start with the basic structure, then gradually add features — no need to describe everything at once

### Tips: Personal Prompt Habits

- Start with `#zh_tw` to force Traditional Chinese output
- Specify the programming language and framework
- List features in bullet points

### 1-2. Deployment & Sharing

#### 1-2-1. Deploy to Cloud Run

AI Studio has built-in integration with Google Cloud Run, allowing you to deploy your web app to the internet with one click.

Steps:

1. In the AI Studio interface, click the "**Publish**" button at the top
2. The system will automatically package and deploy the code to Cloud Run
3. After deployment, a public URL will be generated (e.g., `https://xxx.run.app`) — anyone can visit your website through this URL

> *Deployment incurs minor costs (compute + traffic), but we received $5 in Credits earlier at the event, which should be sufficient for normal testing. If you're concerned about costs, you can delete the Cloud Run service from the [Google Cloud Console](https://console.cloud.google.com/) after testing.*

#### 1-2-2. Share Your Workspace

You can share your current workspace (including your prompts and generated code) with others.

Steps:

1. Click the "**Share**" button at the top
2. The system will generate a sharing link
3. Recipients can view your complete workspace and click "**Remix**" to build upon it

Great for: Exchanging results with classmates, letting others continue development based on your work

#### 1-2-3. Download Code

If you want to download the code to your local machine and continue development with your own editor (such as Antigravity):

1. Click the "**Code**" tab at the top to switch to code view mode
2. Click the **Download Icon** on the right
3. A `.zip` file will be downloaded — extract it to open locally

#### 1-2-4. Connect to GitHub

You can also push the code directly to a GitHub Repository for version management and collaboration.

Steps:

1. Click the **gear icon** (Settings) in the top-right corner
2. Find the "**GitHub**" section and click to connect your account
3. Authorize AI Studio to access your GitHub
4. Create the repository you want to push to (choose permissions, etc.)

## Section 2. Build a Website with Antigravity!

Difficulty: ⭐⭐⭐⭐

In Section 1, we used AI Studio to quickly generate a website. Now we'll download the code to our local machine, open the folder with Antigravity, and continue fine-tuning and debugging.

The goal of this section is: Learn to use an AI IDE with Docker to set up a runnable website environment on your local machine.

### 2-1. Open the Project with Antigravity

1. Extract the `.zip` downloaded in Section 1 to a directory of your choice
2. Open Antigravity and select "**Open Folder**" to open that directory
3. Antigravity will automatically recognize the project structure — you can see the file tree on the left

### 2-2. Local Development & Debugging

Here are the commonly used commands for a React + Vite project:

```bash
# Install dependencies
npm install

# Start the development server
npm run dev

# Build the project
npm run build
```

If you can't remember the commands, just run `npm run` to see available scripts,
or check the `package.json` file to see which commands are available.

### 2-3. Set Up the Local Test Environment

Next, we'll use Docker to run the website. Type the following prompt directly in Antigravity's chat window to have AI generate the necessary configuration files:

```text
Write me a Dockerfile and docker-compose.yml, using nginx as the
web server container, mapping port 80 inside the container to port 8080
on the host machine
```

> The AI-generated content may differ for each person — this is normal.
> As long as you can ultimately run `docker-compose up -d`, that's all that matters.

### 2-4. Manually Add Files (If AI Generation Has Issues)

<details>
<summary>Click to expand: Full contents of manual files</summary>

If the AI-generated files have errors or are missing, you can manually create the following files:

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

### 2-5. Remember to Set `GEMINI_API_KEY`

On the AI Studio page, find the "Get API key" section in the bottom-left corner.
Click `Create API key` to generate an API Key.

https://aistudio.google.com/api-keys

Copy `.env.sample` to `.env` and fill in the `GEMINI_API_KEY`:

```text
GEMINI_API_KEY="MY_GEMINI_API_KEY"
```

### Troubleshooting: I Can't See the Website

Check if there is an error in the `vite.config.ts` at the project root:

```javascript
export default defineConfig(({mode}) => {
  const env = loadEnv(mode, '.', '');
  return {

    base: './',  // <-- Add this part

  };
});
```

### Note: How to Remove `GEMINI_API_KEY`

If you're not using any Gemini features, how do you remove the `GEMINI_API_KEY`?
Find the `vite.config.ts` file and remove the `process.env.GEMINI_API_KEY` section:

```javascript
export default defineConfig(({mode}) => {
  const env = loadEnv(mode, '.', '');
  return {
    // Remove this section
    define: {
      'process.env.GEMINI_API_KEY': JSON.stringify(env.GEMINI_API_KEY),
    },

  };
});
```

### 2-4. Container Operations

Once all files are ready, execute the following commands in the terminal at the project root:

Start the container (with rebuild):

```bash
docker compose up -d --build
```

After success, open your browser and go to http://localhost:8080/
You should see your website.

Other commonly used commands:

```bash
# Stop the container
docker compose down

# View logs (very useful for debugging)
docker compose logs

# Enter the container for debugging (you can use ls, cat, etc. to inspect files)
docker compose exec -it web sh
```

> After each code modification, you need to re-run `docker-compose up -d --build` to see the changes.

## Section 3. Red Team Mindset: Penetration Testing with PentestGPT

> ⚠️ Disclaimer: The following tools are strictly limited to authorized penetration testing, security research, and educational purposes. Unauthorized testing of systems is illegal.

Difficulty: ⭐⭐⭐⭐⭐

In the previous two sections, we used AI to quickly build a website and deploy it locally. Now we'll switch perspectives — standing in the attacker's shoes, we'll use AI-driven penetration testing tools to check our own website for security vulnerabilities.

This is the concept of "Red Team" in cybersecurity: simulating attacker behavior, proactively finding system weaknesses so we can patch them before a real attack occurs.

Penetration testing tool used in this workshop:
https://github.com/yuhano/PentestGPT-MCP
Modified Docker image:
https://hub.docker.com/r/j796160836/pentestgpt-mcp

### 3-1. Connect PentestGPT-MCP to AI Tools

PentestGPT-MCP is an MCP Server that wraps multiple penetration testing tools (such as nmap and dirb), allowing AI to directly call these tools for automated testing.

Since the installation process is relatively complex, I've modified it to use a simpler installation method.
We need to register PentestGPT-MCP as an MCP Server in the AI tool so the AI can call it.

Below are two methods — choose one:

#### 3-1-1. Method 1: Connect MCP in Antigravity

Steps:

1. Click the "**...**" button in the top-right corner of Antigravity
2. Click "**MCP Servers**" to see the MCP Store screen
3. Click "**Manage MCP Servers**"
4. Click "**View Raw config**" to open the config file `~/.gemini/antigravity/mcp_config.json`

Enter the following JSON:

**Same for macOS / Linux / Windows:**

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

> If you have other mcpServers, add the new server inside the `mcpServers` object, separated by commas.

#### 3-1-2. Method 2: Connect MCP in Gemini CLI

Edit the `.gemini/settings.json` file in your home directory:

**macOS / Linux:**

```bash
vi ~/.gemini/settings.json
```

**Windows (PowerShell):**

```powershell
notepad "$env:USERPROFILE\.gemini\settings.json"
```

Add the `mcpServers` block to the JSON:

**Example:**

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

> If the file already contains other settings (such as `general` or `security`), add `mcpServers` at the same level without overwriting existing settings.

### 3-2. Start Penetration Testing

Confirm that the Docker container from Section 2 is running (http://localhost:8080/ is accessible), then enter the following prompt in Antigravity or Gemini CLI:

**Example:**

```text
Please use the pentest MCP to check if there are any issues with
this URL:

http://localhost:8080/
```

After receiving the command, the AI will automatically call nmap and dirb through MCP to scan and report any discovered issues and recommendations.

### 3-3. Important Notes

- **Local testing only:** The target must always be a `localhost` URL in a closed environment. Unauthorized scanning of external websites may be illegal and risks IP blocking
- **dirb wordlist path:** dirb defaults to looking for `/usr/share/wordlists/dirb/common.txt`. If you want to use a custom wordlist, specify the actual file path in your prompt
- **Scan duration:** Depending on the wordlist size and website complexity, scanning may take several minutes — please be patient

## Bonus: Deploy to Cloud Run with Antigravity

### Deploy to Cloud Run

Steps:

1. Click the "**...**" button in the top-right corner of Antigravity
2. Click "**MCP Servers**" to see the MCP Store screen
3. Install "**CloudRun MCP**"
4. Install [gcloud CLI](https://docs.cloud.google.com/sdk/docs/install-sdk)
5. Log in to your Google account

6. Enter a prompt:

```text
Please deploy this application to Cloud Run
Account: xxxxx@gmail.com
Project: xxxxxxxxxxx

Use the cheapest node option
```

Tips:

- Make sure to specify the account name and project name in the prompt,
otherwise the AI will spend time figuring them out
- Ensure your project has a billing account linked with sufficient balance,
to avoid non-technical issues

### Delete the Cloud Run Deployment

You can also use a prompt to delete the deployment:

```text
Please delete the website that was just deployed
```

Gemini will give you a reminder:

> Tip: To keep your environment clean, I recommend manually going to the Google Cloud Console to delete the container images generated in gcr.io (Artifact Registry) to avoid minor storage costs in the future.

You can search for "Artifact Registry" in Google Cloud:
https://console.cloud.google.com/artifacts

Find the corresponding image and delete it.

## 4. Conclusion & Further Reading (Where do we go from here?)

Congratulations on completing today's workshop! We started from scratch, used AI to generate a website, deployed it to a local environment, and even examined our own work from an attacker's perspective.

Every technology mentioned today has a deep field of study behind it. Below are some directions for you to continue exploring based on your interests:

### Web Development

- **Frontend basics:** Start with HTML / CSS / JavaScript fundamentals, then move on to frameworks like React
- **Backend basics:** Try building a simple API with Node.js (Express) or Python (Flask / FastAPI)
- **Full-stack projects:** Attempt building a complete application with frontend + backend + database

### DevOps / Deployment

- **Advanced Docker:** Learn multi-stage builds, Docker networks, volume mounts
- **CI/CD:** Implement automated testing and deployment with GitHub Actions
- **Cloud platforms:** Explore Google Cloud Run, GCP, and other cloud services in depth

### Cybersecurity

- **OWASP Top 10:** Understand the 10 most common web application security risks
- **CTF practice:** Practice security skills through platforms like [OverTheWire](https://overthewire.org/) and [Hack The Box](https://www.hackthebox.com/)
- **Vulnerability remediation:** Learn how to defend against XSS, SQL Injection, CSRF, and other attacks

### AI-Assisted Development

- **Prompt Engineering:** Learn how to communicate more effectively with AI to improve output quality
- **MCP ecosystem:** Explore more MCP Servers to enable AI to operate more tools
- **AI Agents:** Understand the concept of AI Agents and build automated development workflows

> Most importantly: **Just do it.** Pick a topic that interests you, use the methods you learned today, and let AI accompany you as you learn and develop.

Thank you for participating in this workshop. Wishing you continued growth in the AI era! 🚀

---

## LICENSE

MIT
