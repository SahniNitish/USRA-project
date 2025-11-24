# Website Builder AI

An AI-powered website builder that generates complete web applications from natural language prompts using Claude AI and WebContainer technology.

## Overview

Website Builder AI allows users to describe their desired website in plain English, and the application generates a complete, working website with proper file structure, code, and live preview. The system uses Claude AI to understand user requirements and generate appropriate code, while WebContainer provides an in-browser Node.js runtime for instant previews.

## Features

- 🤖 **AI-Powered Generation**: Uses Claude AI to interpret prompts and generate code
- 📁 **File Explorer**: Interactive file tree for navigating generated files
- 💻 **Code Editor**: Monaco editor integration for viewing generated code
- 👁️ **Live Preview**: Real-time preview using WebContainer technology
- 🔄 **Iterative Development**: Continue refining your project with follow-up prompts
- 📋 **Step-by-Step Process**: Visual tracking of build steps and progress

## Tech Stack

### Frontend
- **React 18** with TypeScript
- **Vite** for build tooling
- **React Router** for navigation
- **TailwindCSS** for styling
- **Monaco Editor** for code viewing
- **WebContainer API** for in-browser runtime
- **Lucide React** for icons

### Backend
- **Node.js** with Express
- **TypeScript**
- **Anthropic Claude API** (Claude 3.5 Sonnet)
- **CORS** enabled for cross-origin requests

## Project Structure

```
project/
├── be/                          # Backend server
│   ├── src/
│   │   ├── index.ts            # Main server file
│   │   ├── prompts.ts          # System prompts for Claude
│   │   ├── constants.ts        # Configuration constants
│   │   ├── stripindents.ts     # Utility functions
│   │   └── defaults/           # Default templates
│   │       ├── node.ts         # Node.js template
│   │       └── react.ts        # React template
│   ├── package.json
│   └── tsconfig.json
│
└── frontend/                    # React frontend
    ├── src/
    │   ├── components/         # React components
    │   │   ├── CodeEditor.tsx
    │   │   ├── FileExplorer.tsx
    │   │   ├── PreviewFrame.tsx
    │   │   ├── StepsList.tsx
    │   │   └── TabView.tsx
    │   ├── pages/             # Page components
    │   │   ├── Home.tsx
    │   │   └── Builder.tsx
    │   ├── hooks/             # Custom React hooks
    │   │   └── useWebContainer.ts
    │   ├── types/             # TypeScript types
    │   ├── steps.ts           # XML parsing utilities
    │   ├── config.ts          # Configuration
    │   └── App.tsx            # Main app component
    ├── package.json
    └── vite.config.ts
```

## Installation

### Prerequisites
- Node.js (v18 or higher)
- npm or yarn
- Anthropic API key

### Backend Setup

1. Navigate to the backend directory:
```bash
cd be
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file:
```bash
cp .env.example .env
```

4. Add your Anthropic API key to `.env`:
```
ANTHROPIC_API_KEY=your_api_key_here
```

5. Build and start the server:
```bash
npm run dev
```

The backend server will start on `http://localhost:3000`

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

The frontend will start on `http://localhost:5173`

## Usage

1. **Start the Application**: Ensure both backend and frontend servers are running

2. **Enter Your Prompt**: On the home page, describe the website you want to build
   - Example: "Create a todo list app with React and Tailwind CSS"
   - Example: "Build a landing page for a coffee shop"

3. **View Generated Steps**: The AI will break down the project into steps:
   - File creation
   - Code generation
   - Dependencies installation

4. **Explore the Code**: 
   - Use the file explorer to navigate through generated files
   - View code in the Monaco editor
   - See syntax highlighting and proper formatting

5. **Preview Your Site**: Switch to the Preview tab to see your website running live

6. **Iterate**: Send additional prompts to refine or add features to your project

## API Endpoints

### POST `/template`
Determines the project template (Node.js or React) based on the prompt.

**Request Body:**
```json
{
  "prompt": "your project description"
}
```

**Response:**
```json
{
  "prompts": ["system prompts array"],
  "uiPrompts": ["ui initialization prompts"]
}
```

### POST `/chat`
Processes user messages and generates code responses.

**Request Body:**
```json
{
  "messages": [
    {
      "role": "user",
      "content": "message content"
    }
  ]
}
```

**Response:**
```json
{
  "response": "AI-generated XML response with code"
}
```

## How It Works

1. **Prompt Analysis**: User prompt is sent to Claude AI to determine project type (Node.js or React)

2. **Template Selection**: System loads appropriate base template with necessary dependencies

3. **Code Generation**: Claude generates structured XML responses with file contents:
```xml
<boltArtifact id="project" title="Project Files">
  <boltAction type="file" filePath="src/App.tsx">
    // code content
  </boltAction>
  <boltAction type="shell">
    npm install
  </boltAction>
</boltArtifact>
```

4. **XML Parsing**: Frontend parses XML to extract steps and file structure

5. **File System Creation**: Files are created in WebContainer's virtual file system

6. **Live Preview**: WebContainer runs the development server and displays preview

## Configuration

### Backend Configuration (`be/src/constants.ts`)
- `WORK_DIR`: Working directory for projects
- `allowedHTMLElements`: Allowed HTML elements in responses

### Frontend Configuration (`frontend/src/config.ts`)
- `BACKEND_URL`: Backend API endpoint

### Vite Configuration (`frontend/vite.config.ts`)
WebContainer requires specific headers:
```typescript
server: {
  headers: {
    "Cross-Origin-Embedder-Policy": "require-corp",
    "Cross-Origin-Opener-Policy": "same-origin"
  }
}
```

## Development

### Building for Production

**Backend:**
```bash
cd be
npm run build
```

**Frontend:**
```bash
cd frontend
npm run build
```

### Linting

**Frontend:**
```bash
npm run lint
```

## Limitations

- WebContainer only supports browser-compatible packages
- Python support limited to standard library only
- No native binary execution
- Git is not available in WebContainer
- Some npm packages requiring native modules won't work

## Troubleshooting

### WebContainer not loading
- Ensure proper CORS headers are set
- Check browser console for errors
- Verify WebContainer API is properly initialized

### Preview not showing
- Check if npm install completed successfully
- Verify dev server started (check console logs)
- Ensure port is not blocked

### Backend connection issues
- Verify backend is running on port 3000
- Check CORS configuration
- Ensure API key is valid

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

ISC License

## Credits

Built with:
- [Anthropic Claude API](https://www.anthropic.com/)
- [WebContainer API](https://webcontainers.io/)
- [Monaco Editor](https://microsoft.github.io/monaco-editor/)
- [React](https://react.dev/)
- [Vite](https://vitejs.dev/)

## Support

For issues, questions, or suggestions, please open an issue on the repository.
