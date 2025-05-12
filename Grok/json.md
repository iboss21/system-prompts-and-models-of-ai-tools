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
