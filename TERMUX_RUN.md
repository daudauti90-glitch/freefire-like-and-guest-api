# Termux Setup & Run Guide (Educational/Legal Use)

Ye guide aapke repo ko **Termux (Android)** me run karne ke liye hai.

## 1) Termux packages install karo
```bash
pkg update -y && pkg upgrade -y
pkg install -y git python rust clang libffi openssl
```

> Note: Kuch Python wheels Android/ARM pe direct nahi milte, isliye `clang/rust/libffi/openssl` helpful hote hain build ke liye.

## 2) Storage permission do
```bash
termux-setup-storage
```
Isse `/storage/emulated/0` access milta hai.

## 3) Repo clone karo
```bash
cd ~
git clone <YOUR_REPO_URL> freefire-like-and-guest-api
cd freefire-like-and-guest-api
```

## 4) Virtual environment banao
```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip setuptools wheel
```

## 5) Dependencies install karo
```bash
pip install -r requirements.txt
```
Agar fail aaye to yeh try karo:
```bash
pip install --no-cache-dir httpx protobuf pycryptodome
```

## 6) Basic scripts run karke verify karo
```bash
python count_likes.py
python guests_manager/count_guest.py
```

## 7) Main script run
```bash
python send_like.py
```

---

## Common Termux issues

### A) `ModuleNotFoundError`
- Check karo ki venv active hai: `which python`
- Reinstall deps: `pip install -r requirements.txt`

### B) `Permission denied` / file write issue
- `termux-setup-storage` dubara run karo.
- Paths check karo (especially `guests_manager/*.json`).

### C) Crypto/Protobuf build errors
```bash
pkg install -y clang rust libffi openssl
pip install --upgrade pip setuptools wheel
pip install --no-cache-dir pycryptodome protobuf
```

### D) Frida hooks Termux me directly nahi chal rahe
- Frida workflow ke liye usually:
  - ya to rooted device + frida-server,
  - ya desktop/laptop host machine se attach flow
- Agar sirf Python API scripts test karne hain to Termux ka setup enough hai.

---

## Quick one-shot command block
```bash
pkg update -y && pkg upgrade -y && \
pkg install -y git python rust clang libffi openssl && \
termux-setup-storage && \
cd ~ && git clone <YOUR_REPO_URL> freefire-like-and-guest-api && \
cd freefire-like-and-guest-api && \
python -m venv .venv && source .venv/bin/activate && \
python -m pip install --upgrade pip setuptools wheel && \
pip install -r requirements.txt && \
python guests_manager/count_guest.py
```

Agar aap chaaho to main aapke liye **Termux-compatible `run.sh`** bhi bana du jise ek command se execute kar sako.
