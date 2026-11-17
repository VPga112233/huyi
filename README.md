# 🛡️ PixelShield Backend — Setup & Installation Guide

This guide explains how to extract, install, and run the **PixelShield Backend Engine** (`pixelshield-backend.zip`).

---

## 📋 Prerequisites

- **Python 3.10+** (Recommended: Python 3.11, 3.12, or 3.13)
  - Verify by running: `python --version` in terminal.
- **pip** (comes bundled with Python)

---

## 🚀 Quick Setup (3 Steps)

### Step 1: Unzip the Archive

- **Windows**: Right-click `pixelshield-backend.zip` → **Extract All...** → Click **Extract**.
- **Mac / Linux**: Double-click the `.zip` file, or run:
  ```bash
  unzip pixelshield-backend.zip
  ```

This will produce a folder named `pixelshield-backend/`.

---

### Step 2: Open Terminal Inside the Folder

Open your terminal or command prompt and navigate into the extracted folder:

```bash
cd pixelshield-backend
```

*(Optional but Recommended)* Create and activate a clean virtual environment:

- **Windows (PowerShell)**:
  ```powershell
  python -m venv .venv
  .\.venv\Scripts\activate
  ```
  *(If PowerShell shows a script execution error, run: `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` then activate again)*

- **Windows (Command Prompt / CMD)**:
  ```cmd
  python -m venv .venv
  .venv\Scripts\activate.bat
  ```

- **Mac / Linux**:
  ```bash
  python3 -m venv .venv
  source .venv/bin/activate
  ```

---

### Step 3: Install Dependencies

Run:

```bash
pip install -r requirements.txt
```

*(If you are on a system without GPU, CPU PyTorch and all dependencies will install automatically in ~15-30 seconds).*

---

## ⚡ Start the Backend Server

Run:

```bash
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

When successful, your terminal will display:

```
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Application startup complete.
```

---

## 🔍 Verify & Test

Once the server is running, open these in your browser:

1. **Interactive Swagger Documentation**:  
   👉 **`http://localhost:8000/docs`**  
   *(You can test all 20 API endpoints live with buttons, upload images, test cloaking, run forensics, and generate legal notices).*

2. **OpenAPI Schema (For Frontend Code Generation)**:  
   👉 **`http://localhost:8000/openapi.json`**

3. **System Diagnostics**:  
   👉 **`http://localhost:8000/api/v1/health/`**

4. **Run Automated Test Suite (Optional)**:  
   In a separate terminal inside `pixelshield-backend/`, run:
   ```bash
   pytest -v
   ```
   All **23 unit & integration tests** will pass with green checkmarks.

---

## 🌐 Connecting Your Frontend

- **Base API URL**: `http://localhost:8000/api/v1`
- **CORS**: Already enabled for all origins (`*`). Your frontend on `localhost:3000` (React/Next.js) or `localhost:5173` (Vite) can send requests directly without CORS issues.

### Key API Routes for Frontend UI:
- **Adversarial Cloaking**: `POST /api/v1/protect/cloak` *(multipart/form-data: `file`, `preset`)*
- **Stress Test Simulator**: `POST /api/v1/protect/stress-test` *(multipart/form-data: `original_file`, `cloaked_file`)*
- **"Is This Picture Fake?" Forensics**: `POST /api/v1/forensics/analyze` *(multipart/form-data: `file`)*
- **Legal Takedown Notice**: `POST /api/v1/respond/takedown/generate` *(FormData: `platform`, `platform_url`, `perpetrator_handle`)*
- **Section 65B Evidence Vault**: `POST /api/v1/respond/evidence/seal` *(multipart/form-data: `evidence_file`, `incident_type`)*
- **Blackmail SOS Emergency**: `POST /api/v1/respond/sos/initiate` *(JSON: `blackmailer_handle`, `trusted_contacts`)*

---

## ❓ Troubleshooting

| Issue | Solution |
|---|---|
| `uvicorn: command not found` | Ensure virtual environment is activated (`.\.venv\Scripts\activate` or `source .venv/bin/activate`), or run via `python -m uvicorn app.main:app --reload` |
| Windows PowerShell Script Execution error | Run `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` |
| Port 8000 already in use | Run on another port: `uvicorn app.main:app --reload --port 8001` |
