# 🔐 IoT Secure System — Attribute-Based Encryption

A complete IoT security architecture using **Hybrid Attribute-Based Encryption (ABE)** combined with AES symmetric encryption, managed through a Flask web dashboard.

---

## 📁 Project Structure

```
projet_abe/
├── Cloud/
│   └── cloud.py          # Flask app + global ABE authority + dashboard
├── IoT/
│   └── capteur.py        # IoT sensor simulation
├── User/
│   └── user.py           # User management
├── schemas/
│   ├── kp_abe.py         # Hybrid KP-ABE + AES
│   └── cp_abe.py         # Hybrid CP-ABE + AES
├── main.py               # Entry point
├── requirements.txt      # Python dependencies
└── Dockerfile
```

---

## 🔑 Cryptographic Architecture

| Role | KP-ABE | CP-ABE |
|------|--------|--------|
| **Authority** | `setup()` → `(KP_PK, KP_MK)` global | `setup()` → `(CP_PK, CP_MK)` global |
| **Sensor** | `encrypt(pk, data, ATTRIBUTES)` | `encrypt(pk, data, POLICY)` |
| **User** | `keygen(pk, mk, POLICY)` | `keygen(pk, mk, ATTRIBUTES)` |
| **Decrypt** | `decrypt(ct, sk)` | `decrypt(pk, sk, ct)` |

---

## 🐳 Option 1 — Run with Docker (Recommended)

### Pull the image

```bash
docker pull bahida2026youssef/iot-abe-encrypt:latest
```

### Run the container

```bash
docker run -p 5000:5000 bahida2026youssef/iot-abe-encrypt:latest
```

### Open the dashboard

```
http://localhost:5000
```

> ✅ No installation needed — everything is inside the image.

---

## 🐍 Option 2 — Run Locally (Manual)

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO/projet_abe
```

### 2. Create a virtual environment

```bash
python -m venv env
source env/bin/activate        # Linux / Mac
env\Scripts\activate           # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

> ⚠️ `charm-crypto-framework` requires **GMP** and **PBC** libraries.
> On Ubuntu/Debian:
> ```bash
> sudo apt install libgmp-dev libssl-dev flex bison wget
> ```
> PBC must be compiled from source — see [Dockerfile](./Dockerfile) for reference.

### 4. Run the app

```bash
python Cloud/cloud.py
```

### 5. Open the dashboard

```
http://127.0.0.1:5000
```

---

## 🖥️ How to Use the Dashboard

### Step 1 — Add a Sensor
```
Sensor ID   →  S1
Scheme      →  KP-ABE  or  CP-ABE
Attributes  →  ONE, TWO, THREE        (if KP-ABE)
Policy      →  ((ONE or TWO) and THREE)  (if CP-ABE)
Interval    →  5  (seconds)
```

### Step 2 — Add a User
```
User ID     →  alice
Scheme      →  KP-ABE  or  CP-ABE
Policy      →  ((ONE or TWO) and THREE)  (if KP-ABE)
Attributes  →  ONE, TWO, THREE           (if CP-ABE)
```

### Step 3 — Watch encrypted records appear automatically every 5 seconds

### Step 4 — Decrypt a record
```
Select a record  →  Select a user  →  Click Decrypt
→  Raw sensor JSON appears  ✅
```

---

## 🛠️ Tech Stack

| Technology | Role |
|---|---|
| Python 3.10 | Core language |
| charm-crypto-framework | KP-ABE & CP-ABE (SS512 curve) |
| Flask | Web dashboard |
| coapthon3 | CoAP protocol (IoT gateway) |
| AES | Symmetric encryption (hybrid scheme) |
| Docker | Containerization |

---

## 🐳 Docker Hub

```
Image   :  bahida2026youssef/iot-abe-encrypt:latest
Pull    :  docker pull bahida2026youssef/iot-abe-encrypt:latest
Run     :  docker run -p 5000:5000 bahida2026youssef/iot-abe-encrypt:latest
```

🔗 [View on Docker Hub](https://hub.docker.com/r/bahida2026youssef/iot-abe-encrypt)
