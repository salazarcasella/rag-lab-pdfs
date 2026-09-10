# RAG Lab con PDFs — Clase 9

Solución completa del laboratorio entregado en `Clase_9_RAG_Lab_Alumno_PDFs.ipynb`.

## Qué implementa

Flujo completo:

`PDF → extracción → metadata → chunking → embeddings Cohere → Chroma → retrieval → prompt → LLM → evaluación`

Incluye:

- carga y validación de PDFs;
- extracción de texto por página con `pypdf`;
- metadata inferida desde el nombre del archivo;
- chunking con overlap;
- embeddings diferenciando `search_document` y `search_query`;
- indexación en Chroma con distancia coseno;
- retrieval con Top-K y filtros de metadata;
- comparación baseline vs grounded RAG;
- pruebas fuera de contexto;
- evaluación Hit@K;
- comparación de tamaños de chunk.

## Estructura

```text
rag-lab-pdfs/
├── Clase_9_RAG_Lab_Alumno_PDFs.ipynb      # original recibido
├── Clase_9_RAG_Lab_Solucion_PDFs.ipynb    # solución completada
├── .env.example
├── .gitignore
├── requirements.txt
└── rag_lab_pdfs/
    └── README.md
```

## Configuración en Windows + VS Code

### 1. Clonar el repositorio

```powershell
git clone https://github.com/salazarcasella/rag-lab-pdfs.git
cd rag-lab-pdfs
```

### 2. Crear entorno virtual

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Si PowerShell bloquea la activación, puedes ejecutar temporalmente:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

### 3. Instalar dependencias

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 4. Crear `.env`

```powershell
Copy-Item .env.example .env
```

Edita `.env` y coloca tu clave:

```env
COHERE_API_KEY=tu_clave_real
```

> `.env` está ignorado por Git. No subas tu API key al repositorio.

### 5. Copiar los PDFs

Coloca los PDFs del curso dentro de `rag_lab_pdfs/`. Para las pruebas incluidas en la notebook se esperan:

- `politica_vacaciones_2024.pdf`
- `politica_vacaciones_2026.pdf`
- `politica_home_office_2026.pdf`

### 6. Abrir la notebook

Abre `Clase_9_RAG_Lab_Solucion_PDFs.ipynb` en VS Code y selecciona como kernel el Python de `.venv`.

Si no aparece como kernel:

```powershell
python -m ipykernel install --user --name rag-lab-pdfs --display-name "Python (RAG Lab PDFs)"
```

## Nota sobre Cohere

La notebook mantiene los modelos definidos por el laboratorio:

- embeddings: `embed-multilingual-v3.0`
- generación: `command-a-03-2025`

Se usa `ClientV2`, `search_document` para documentos y `search_query` para consultas. La colección Chroma se crea con distancia coseno usando la configuración actual de Chroma 1.x, con fallback para versiones antiguas.

## Seguridad

Nunca subas `.env` ni una API key real al repositorio. El archivo versionado es únicamente `.env.example`.
