I understand you’re looking for a comprehensive, professional setup for using me, Grok, as an AI coding agent in Cursor, with a "full spectrum" and "full pro version" configuration. You’ve requested prompts and tools tailored for Grok, provided examples from v0’s prompts and Replit’s tools, and now want setup instructions to integrate these into Cursor for a robust coding environment. Drawing on your previous interactions (e.g., building TheLux app with Next.js and FastAPI, CreditIQ with StarCoder, and a Replit-like agent), I’ll provide a complete setup guide, including enhanced `prompts.md` and `tools.md` files, detailed installation steps, and instructions to maximize my capabilities in Cursor.

This setup will:
- **Leverage Grok’s Features**: Utilize DeepSearch, think mode, and xAI API integration for advanced coding tasks.
- **Support Full-Stack Development**: Focus on modern frameworks (Next.js, FastAPI, React Native) and deployment options (Vercel, Render, self-hosted VPS).
- **Ensure Professional Workflow**: Include tools for file operations, API calls, database management, and secure key handling, tailored for Cursor.
- **Be Production-Ready**: Incorporate security best practices, scalability, and monetization features (e.g., Stripe subscriptions for TheLux).

The response will include two artifacts (`prompts.md` and `tools.md`) wrapped in `<xaiArtifact>` tags with unique UUIDs, as these are new files building on your previous request. I’ll also provide step-by-step setup instructions, addressing your hardware (Intel i9-9900K, RTX 4070, 64GB RAM) and VPS preferences from past conversations, ensuring a pro-level configuration.

---

### Setup Instructions for Grok as AI Coding Agent in Cursor

#### 1. Install and Configure Cursor
- **Download Cursor**: Install Cursor from [cursor.com](https://cursor.com) for your OS (Windows, macOS, or Ubuntu, per your April 7, 2025, preference for Linux).
- **Verify Dependencies**:
  ```bash
  node -v  # Ensure Node.js v20+ (e.g., v20.12.2)
  python --version  # Ensure Python 3.10+ (e.g., 3.11)
  docker -v  # Optional for containerized deployment
  ```
  Install if missing:
  ```bash
  sudo apt update
  sudo apt install nodejs npm python3 python3-pip docker.io
  ```
- **Set Up Cursor**:
  - Open Cursor and sign in.
  - Go to Settings > AI Providers, select Grok, and enter your xAI API key (obtain from [x.ai/api](https://x.ai/api)).
  - Enable terminal and file explorer integrations in Cursor’s settings.

#### 2. Create Project Structure
- **Initialize Project**:
  ```bash
  mkdir my-codemaster
  cd my-codemaster
  npm init -y
  npx create-next-app@latest src --ts --tailwind --eslint --app
  ```
  Choose defaults for Next.js setup (App Router, TypeScript, Tailwind).
- **Add Dependencies**:
  ```bash
  npm install @ai-sdk/xai @ai-sdk/openai shadcn-ui lucide-react
  pip install fastapi uvicorn python-dotenv supabase
  ```
- **Directory Structure**:
  ```
  my-codemaster/
  ├── src/                  # Next.js frontend
  │   ├── app/
  │   ├── components/
  │   └── lib/
  ├── api/                  # FastAPI backend
  │   ├── main.py
  │   └── requirements.txt
  ├── prompts.md            # Grok prompts
  ├── tools.md             # Grok tools
  ├── .env                 # Environment variables
  └── README.md
  ```

#### 3. Save Prompts and Tools
- Create `prompts.md` and `tools.md` in the project root using the artifacts below.
- These files define my behavior and capabilities, optimized for Cursor’s environment.

#### 4. Configure Environment Variables
- Create `.env` in the project root:
  ```env
  XAI_API_KEY=your_xai_api_key
  OPENAI_API_KEY=your_openai_api_key
  HUGGINGFACE_API_KEY=your_huggingface_api_key
  SUPABASE_URL=your_supabase_url
  SUPABASE_KEY=your_supabase_key
  DATABASE_URL=postgresql://user:password@localhost:5432/mydb
  NEXT_PUBLIC_API_URL=http://localhost:8000
  ```
- Secure keys (per March 28, 2025):
  ```bash
  chmod 600 .env
  ```
- Load in FastAPI (`api/main.py`):
  ```python
  from dotenv import load_dotenv
  import os
  load_dotenv()
  XAI_API_KEY = os.getenv("XAI_API_KEY")
  ```

#### 5. Set Up FastAPI Backend
- Create `api/main.py`:
  ```python
  from fastapi import FastAPI
  from pydantic import BaseModel
  from ai import generateText
  from ai_sdk.xai import xai

  app = FastAPI()

  class CodeRequest(BaseModel):
      prompt: str

  @app.post("/code")
  async def generate_code(request: CodeRequest):
      response = await generateText({
          "model": xai("grok-3"),
          "prompt": request.prompt
      })
      return {"code": response.text}
  ```
- Create `api/requirements.txt`:
  ```
  fastapi
  uvicorn
  python-dotenv
  ai
  ai-sdk-xai
  ```
- Run the backend:
  ```bash
  cd api
  pip install -r requirements.txt
  uvicorn main:app --reload
  ```

#### 6. Integrate with Cursor
- **Use Prompts**:
  - In Cursor, open a new file and write a prompt using `prompts.md` syntax:
    ```md
    <thinking>
    - Create a login page with shadcn/ui
    - Use write_to_file for src/app/login/page.tsx
    - Check XAI_API_KEY
    </thinking>
    ```
  - Cursor will process the prompt using my API, generating code or executing tools.
- **Execute Tools**:
  - Call tools via JSON in Cursor:
    ```json
    {
      "tool": "write_to_file",
      "parameters": {
        "path": "src/app/page.tsx",
        "content": "export default function Home() { return <h1>Hello, Grok!</h1>; }"
      }
    }
    ```
  - Cursor will save the file to the specified path.
- **Preview Code**:
  - Open `src/app/page.tsx` in Cursor to preview Next.js components.
  - Run `npm run dev` in Cursor’s terminal to see the live app at `http://localhost:3000`.

#### 7. Test and Debug
- **Unit Tests**:
  Create `tests/test_api.py`:
  ```python
  import unittest
  from fastapi.testclient import TestClient
  from api.main import app

  class TestCodeMaster(unittest.TestCase):
      def setUp(self):
          self.client = TestClient(app)

      def test_generate_code(self):
          response = self.client.post("/code", json={"prompt": "Create a React component"})
          self.assertEqual(response.status_code, 200)
          self.assertIn("code", response.json())

  if __name__ == "__main__":
      unittest.main()
  ```
  Run:
  ```bash
  python -m unittest tests/test_api.py
  ```
- **Live Testing**:
  ```bash
  curl -X POST http://localhost:8000/code -H "Content-Type: application/json" -d '{"prompt": "Generate a Next.js page"}'
  ```
- **Debugging** (per March 28, 2025):
  - Check `.env` for correct keys.
  - Verify API responses in Cursor’s console.

#### 8. Deploy the Project
- **Vercel (Frontend)**:
  ```bash
  cd src
  vercel --prod
  ```
- **Render (Backend)**:
  - Create a new web service on [render.com](https://render.com).
  - Link your GitHub repo, set `api` as the root directory, and add environment variables.
  - Deploy with:
    ```bash
    Build Command: pip install -r requirements.txt
    Start Command: uvicorn main:app --host 0.0.0.0 --port $PORT
    ```
- **Self-Hosted VPS** (per April 7, 2025):
  - On your KVM VPS with AMD EPYC and NVMe:
    ```bash
    sudo apt update
    sudo apt install nginx docker.io
    ```
  - Build and run Docker container:
    ```dockerfile
    # api/Dockerfile
    FROM python:3.11
    WORKDIR /app
    COPY requirements.txt .
    RUN pip install -r requirements.txt
    COPY . .
    CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
    ```
    ```bash
    cd api
    docker build -t codemaster-api .
    docker run -d -p 8000:8000 --env-file ../.env codemaster-api
    ```
  - Configure Nginx:
    ```nginx
    # /etc/nginx/sites-available/codemaster
    server {
        listen 80;
        server_name your-domain.com;
        location / {
            proxy_pass http://localhost:8000;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
    ```
    ```bash
    sudo ln -s /etc/nginx/sites-available/codemaster /etc/nginx/sites-enabled/
    sudo systemctl restart nginx
    sudo certbot --nginx -d your-domain.com
    ```
- **Local Machine** (Intel i9-9900K, RTX 4070, Ubuntu):
  - Follow the same Docker and Nginx steps as above, running on your local Ubuntu setup to avoid VPS costs (per April 7, 2025).

#### 9. Enhance with Pro Features
- **Subscription Tiers** (per March 10, 2025, for TheLux):
  Add Stripe to `api/main.py`:
  ```python
  import stripe
  stripe.api_key = os.getenv("STRIPE_API_KEY")

  @app.post("/subscribe")
  async def create_subscription(user_id: str, plan: str):
      return stripe.Subscription.create(
          customer=user_id,
          items=[{"price": "price_pro_15" if plan == "pro" else "price_enterprise_35"}]
      )
  ```
- **Real-Time Collaboration** (per April 7, 2025):
  Use Supabase for live updates:
  ```python
  from supabase import create_client
  supabase = create_client(os.getenv("SUPABASE_URL"), os.getenv("SUPABASE_KEY"))

  @app.post("/collaborate")
  async def update_code(file_path: str, content: str):
      supabase.table("code").upsert({"path": file_path, "content": content}).execute()
  ```
- **Analytics** (per March 10, 2025):
  Integrate PostHog in `src/app/layout.tsx`:
  ```tsx
  import { PostHogProvider } from "posthog-js/react";
  export default function RootLayout({ children }) {
    return (
      <PostHogProvider apiKey={process.env.NEXT_PUBLIC_POSTHOG_KEY}>
        {children}
      </PostHogProvider>
    );
  }
  ```

#### 10. Security Best Practices
- **Secure Keys** (per March 28, 2025):
  Use `.gitignore`:
  ```gitignore
  .env
  ```
- **Authentication** (per April 7, 2025):
  Add Supabase auth to `api/main.py`:
  ```python
  def authenticate_user(email: str, password: str):
      return supabase.auth.sign_in_with_password({"email": email, "password": password})
  ```
- **HTTPS**: Ensure Nginx uses Let’s Encrypt (as above).
- **Audits**: Schedule security checks with tools like ZeroLeaks.

---

### prompts.md

This enhanced prompt defines my full-spectrum capabilities, including advanced planning, multi-framework support, and integration with Cursor’s pro features.


## Core Identity
- You are Grok, created by xAI, a professional AI coding agent for Cursor, designed for full-stack development and production-ready solutions.

## Instructions
You are an advanced coding assistant, leveraging xAI’s latest AI capabilities for web, mobile, and backend development. Your responses use Markdown with XML-like tags (`<thinking>`, `<message_user>`) for structured workflows. You default to Next.js App Router, FastAPI, or React Native, ensuring scalable, secure, and monetizable applications.

### General Guidelines
1. **Project Scope**: Support full-stack projects with Next.js, FastAPI, React Native, TypeScript, and Python. Use Tailwind CSS, shadcn/ui, and Lucide React for UI.
2. **Code Standards**: Write modular, type-safe code (ES6+, PEP 8). Include comments and documentation for production use.
3. **Security**: Store API keys in `.env`, use HTTPS, and implement Supabase authentication. Never expose sensitive data.
4. **Cursor Features**:
   - Use terminal for commands (`npm run dev`).
   - Save files to project directory (`src/app/page.tsx`).
   - Preview React/Next.js in Cursor’s editor.
5. **Grok Capabilities**:
   - **DeepSearch Mode**: When activated, search the web iteratively and cite sources (e.g., `[^1]` for xAI API docs).
   - **Think Mode**: Plan tasks in `<thinking>` tags when activated.
   - **xAI API**: Use `@ai-sdk/xai` for code generation (e.g., `generateText` with `grok-3` model).
6. **Output Structure**:
   - Use Markdown for explanations.
   - Use `<CodeProject>` for multi-file projects with a unique `project_id`.
   - Use `` for standalone files when instructed.

### Available MDX Components
- **`<CodeProject project_id="my-app-123">`**:
  - Groups files for Next.js, React, or FastAPI projects.
  - Example:
    ```md
    <CodeProject project_id="my-app-123">
    ```tsx file="src/app/page.tsx"
    import { Button } from "@/components/ui/button";
    export default function Home() {
      return <Button>Hello, Grok!</Button>;
    }
    ```
    </CodeProject>
    ```
  - Use kebab-case for files (e.g., `login-page.tsx`).
  - Maintain `project_id` across edits.
  - Pre-installed: Tailwind CSS, shadcn/ui, Lucide React.
- **`<DeleteFile file="path" />`**:
  - Deletes a file (e.g., `<DeleteFile file="src/old.tsx" />`).
- **`<MoveFile from="old" to="new" />`**:
  - Moves a file and updates imports (e.g., `<MoveFile from="src/old.tsx" to="src/new.tsx" />`).
- **Markdown**:
  - Use `md project="MyApp" file="README.md" type="markdown"`.
  - Example:
    ```md
    ```md project="MyApp" file="README.md" type="markdown"
    # MyApp
    A full-stack app built with Grok.
    ```
    ```
- **Node.js Executable**:
  - Use `js project="MyApp" file="scripts/run.js" type="nodejs"`.
  - Example:
    ```js project="MyApp" file="scripts/run.js" type="nodejs"
    import fs from "fs";
    console.log(fs.readFileSync("data.txt", "utf-8"));
    ```
- **SQL**:
  - Use `sql project="MyApp" file="init.sql" type="code"`.
  - Example:
    ```sql project="MyApp" file="init.sql" type="code"
    CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(255));
    ```

### Planning
Use `<thinking>` tags to plan:
- List files, tools, and dependencies.
- Address styling, assets, and security.
- Example:
  ```md
  <thinking>
  - Create src/app/login/page.tsx with shadcn/ui
  - Use write_to_file tool
  - Add Supabase auth with call_api
  - Deploy to Vercel with suggest_deploy
  </thinking>
  ```

### Styling
- Import shadcn/ui components (e.g., `from "@/components/ui/button"`).
- Use Tailwind CSS for responsive designs.
- Prefer neutral colors; avoid blue/indigo unless specified.
- Set backgrounds via `<div className="bg-gray-100">`.

### Images and Media
- Use `/placeholder.svg?height={height}&width={width}&query={query}` (e.g., `/placeholder.svg?height=400&width=600&query=modern dashboard`).
- For assets:
  ```md
  ```png file="public/images/hero.png" url="[BLOB_URL]"
  ```
- Use Lucide React icons (e.g., `import { User } from "lucide-react"`).

### AI Integration
- Use xAI API:
  ```js
  import { generateText } from "ai";
  import { xai } from "@ai-sdk/xai";
  const { text } = await generateText({
    model: xai("grok-3"),
    prompt: "Generate a FastAPI endpoint"
  });
  ```
- Check keys with `check_secrets` or prompt with `ask_secrets`.

### Accessibility
- Use semantic HTML (`main`, `nav`).
- Apply ARIA attributes.
- Add `sr-only` for screen reader text.
- Include alt text for images.

### Existing Files
Assume:
- `app/layout.tsx`
- `components/ui/*`
- `lib/utils.ts`
- `app/globals.css`
- `tailwind.config.ts`
Do not regenerate unless requested.

### Deployment
- Use `suggest_deploy` for Vercel, Render, or VPS.
- Example:
  ```bash
  vercel --prod
  ```

### Refusals
For harmful requests:
```md
I'm sorry. I'm not able to assist with that.
```

### Suggested Actions
Suggest 3–5 actions post-task:
```md
<Actions>
  <Action name="Add Supabase auth" description="Integrate Supabase for user login" />
  <Action name="Deploy to Vercel" description="Deploy with `vercel --prod`" />
  <Action name="Add analytics" description="Integrate PostHog for tracking" />
</Actions>
```

## Domain Knowledge
- Cite xAI API docs `[^1]` and Vercel knowledge base `[^vercel_knowledge_base]`.
- Example: “Grok uses xAI API for code generation `[^1]`.”

<sources>
[^1]: [xAI API Documentation](https://x.ai/api)
</sources>


---

### tools.md

This file defines a comprehensive set of tools for full-stack development, including file operations, API calls, database management, and deployment.

```json
{
  "tools": [
    {
      "name": "write_to_file",
      "description": "Write or update a file in the project directory.",
      "parameters": {
        "type": "object",
        "properties": {
          "path": {
            "type": "string",
            "description": "Relative file path (e.g., src/app/page.tsx)"
          },
          "content": {
            "type": "string",
            "description": "Content to write"
          }
        },
        "required": ["path", "content"]
      }
    },
    {
      "name": "execute_command",
      "description": "Run a terminal command in Cursor.",
      "parameters": {
        "type": "object",
        "properties": {
          "command": {
            "type": "string",
            "description": "Command to execute (e.g., npm install)"
          },
          "requires_approval": {
            "type": "boolean",
            "default": true,
            "description": "Require user approval"
          }
        },
        "required": ["command"]
      }
    },
    {
      "name": "call_api",
      "description": "Make an HTTP request to an external API.",
      "parameters": {
        "type": "object",
        "properties": {
          "url": {
            "type": "string",
            "description": "API endpoint URL"
          },
          "method": {
            "type": "string",
            "enum": ["GET", "POST", "PUT", "DELETE"],
            "description": "HTTP method"
          },
          "headers": {
            "type": "object",
            "description": "Request headers"
          },
          "body": {
            "type": "object",
            "description": "Request body"
          }
        },
        "required": ["url", "method"]
      }
    },
    {
      "name": "create_postgresql_database",
      "description": "Create a PostgreSQL database with environment variables.",
      "parameters": {
        "type": "object",
        "properties": {}
      }
    },
    {
      "name": "execute_sql",
      "description": "Run a SQL query on the project’s database.",
      "parameters": {
        "type": "object",
        "properties": {
          "sql_query": {
            "type": "string",
            "description": "SQL query to execute"
          }
        },
        "required": ["sql_query"]
      }
    },
    {
      "name": "ask_secrets",
      "description": "Prompt user for API keys, adding to environment variables.",
      "parameters": {
        "type": "object",
        "properties": {
          "secret_keys": {
            "type": "array",
            "items": { "type": "string" },
            "description": "Keys needed (e.g., ['XAI_API_KEY'])"
          },
          "user_message": {
            "type": "string",
            "description": "Explanation for needing keys"
          }
        },
        "required": ["secret_keys", "user_message"]
      }
    },
    {
      "name": "check_secrets",
      "description": "Check if secrets exist in the environment.",
      "parameters": {
        "type": "object",
        "properties": {
          "secret_keys": {
            "type": "array",
            "items": { "type": "string" },
            "description": "Keys to check"
          }
        },
        "required": ["secret_keys"]
      }
    },
    {
      "name": "suggest_deploy",
      "description": "Suggest deploying to Vercel, Render, or VPS.",
      "parameters": {
        "type": "object",
        "properties": {}
      }
    },
    {
      "name": "report_progress",
      "description": "Summarize completed tasks and ask for next steps.",
      "parameters": {
        "type": "object",
        "properties": {
          "summary": {
            "type": "string",
            "description": "Summary of tasks (max 30 words, ✓ for done, → for in progress)"
          }
        },
        "required": ["summary"]
      }
    },
    {
      "name": "github_collaborate",
      "description": "Create a GitHub pull request for collaboration.",
      "parameters": {
        "type": "object",
        "properties": {
          "repo_name": {
            "type": "string",
            "description": "GitHub repository (e.g., user/repo)"
          },
          "branch": {
            "type": "string",
            "description": "Branch name"
          },
          "file_path": {
            "type": "string",
            "description": "File path to update"
          },
          "content": {
            "type": "string",
            "description": "File content"
          }
        },
        "required": ["repo_name", "branch", "file_path", "content"]
      }
    }
  ]
}
```

---

### Example Usage in Cursor
1. **Generate a Next.js Page**:
   In Cursor, write:
   ```md
   <thinking>
   - Create a dashboard page
   - Use shadcn/ui Card component
   - Save to src/app/dashboard/page.tsx
   - Install dependencies
   </thinking>
   ```json
   {
     "tool": "write_to_file",
     "parameters": {
       "path": "src/app/dashboard/page.tsx",
       "content": "import { Card } from '@/components/ui/card';\nexport default function Dashboard() {\n  return <Card>Dashboard</Card>;\n}"
     }
   }
   {
     "tool": "execute_command",
     "parameters": {
       "command": "npm install"
     }
   }
   ```
   Cursor will save the file and run the command.

2. **Deploy to Vercel**:
   ```md
   <thinking>
   - Project is ready
   - Suggest Vercel deployment
   </thinking>
   ```json
   {
     "tool": "suggest_deploy",
     "parameters": {}
   }
   ```
   ```md
   <message_user>
   Run `vercel --prod` in Cursor’s terminal to deploy.
   </message_user>
   ```

3. **Add Supabase Auth**:
   ```md
   <thinking>
   - Check SUPABASE_KEY
   - Add auth endpoint to api/main.py
   </thinking>
   ```json
   {
     "tool": "check_secrets",
     "parameters": {
       "secret_keys": ["SUPABASE_KEY"]
     }
   }
   {
     "tool": "write_to_file",
     "parameters": {
       "path": "api/main.py",
       "content": "from supabase import create_client\nsupabase = create_client(os.getenv('SUPABASE_URL'), os.getenv('SUPABASE_KEY'))\n@app.post('/auth')\nasync def auth(email: str, password: str):\n    return supabase.auth.sign_in_with_password({'email': email, 'password': password})"
     }
   }
   ```

---

### Why This Setup?
- **Full Spectrum**: Covers frontend (Next.js), backend (FastAPI), database (PostgreSQL), and deployment (Vercel, VPS).
- **Pro Version**: Includes monetization (Stripe), collaboration (GitHub), and analytics (PostHog), aligning with your TheLux and CreditIQ goals.
- **Grok-Optimized**: Leverages DeepSearch, think mode, and xAI API for superior code generation.
- **Secure and Scalable**: Implements Supabase auth, HTTPS, and secure key management.

If you want to focus on a specific project (e.g., TheLux with subscriptions, CreditIQ with DisputeGenAI, or a Replit clone), I can generate a tailored `<CodeProject>` or refine the tools. Let me know your next steps or any specific features you’d like to add!
