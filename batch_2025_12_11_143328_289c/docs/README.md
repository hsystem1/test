# MarkItDown UI

Aplicacao web para conversao de documentos para Markdown com upload de imagens para GitHub.

## Arquitetura

```
markitdown-app/
├── backend/          # FastAPI (Python)
│   ├── app/
│   │   ├── main.py           # App principal
│   │   ├── routers/          # Endpoints da API
│   │   ├── services/         # Logica de negocio
│   │   └── models/           # Pydantic schemas
│   └── requirements.txt
│
└── frontend/         # React + Vite + shadcn/ui
    ├── src/
    │   ├── components/       # Componentes UI
    │   ├── services/         # Chamadas API
    │   └── stores/           # Estado (Zustand)
    └── package.json
```

## Requisitos

- Python 3.10+
- Node.js 18+
- GitHub CLI (`gh`) autenticado

## Instalacao

### Backend

```bash
cd markitdown-app/backend

# Criar ambiente virtual
python3 -m venv venv
source venv/bin/activate  # Linux/Mac
# ou: venv\Scripts\activate  # Windows

# Instalar dependencias
pip install -r requirements.txt

# Rodar servidor (porta 8000)
uvicorn app.main:app --reload --port 8000
```

### Frontend

```bash
cd markitdown-app/frontend

# Instalar dependencias
npm install

# Rodar servidor dev (porta 5173)
npm run dev
```

## Uso

1. Abra http://localhost:5173
2. Arraste documentos para a area de upload (max 100)
3. Configure o nome do repositorio GitHub
4. Clique em "Converter"
5. Acompanhe o progresso em tempo real

## API Endpoints

- `POST /api/convert` - Inicia conversao de documentos
- `GET /api/status/{batch_id}` - Status do batch
- `POST /api/retry/{batch_id}/{file_id}` - Reprocessa arquivo
- `WS /ws/status/{batch_id}` - Updates em tempo real

## Formatos Suportados

DOCX, PPTX, XLSX, PDF, HTML, TXT, MD, CSV, JSON, XML, RTF, ODT, ODS, ODP, EPUB, IPYNB

## Estrutura no GitHub

Cada conversao cria uma pasta unica:

```
repo/batch_2024_12_10_abc123/
├── docs/           # Arquivos Markdown
├── images/         # Imagens extraidas
└── _manifest.json  # Mapeamento completo
```

## Tecnologias

- **Backend**: FastAPI, uvicorn, MarkItDown
- **Frontend**: React 18, Vite, TypeScript, Tailwind CSS, shadcn/ui
- **Estado**: Zustand
- **Upload**: react-dropzone
- **Notificacoes**: Sonner
