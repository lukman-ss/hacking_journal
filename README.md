# Hacking Roadmap (Beginner → Expert) — Progress Checklist (hacking-jurnal)

> Fokus: kompetensi + proyek + bukti. Checklist ini dipakai tracking harian/mingguan.  
> Scope: mulai dari **fundamental komputer & network** sampai **AppSec/Cloud/Detection** level produksi.  
> Semua latihan **legal**: lab sendiri / CTF / platform training.

## Cara pakai
- Centang item saat **sudah bisa dipraktikkan**, bukan sekadar “sudah baca”.
- Setiap phase wajib punya **bukti output** (repo / catatan / screenshot / demo).
- Semua hasil kerja masuk ke struktur: `notes/`, `labs/`, `runbooks/`, `projects/`.
- Catatan fokus “konsep + observasi + mitigasi”, hindari menulis langkah eksploit rinci.

---

## Struktur Repo
```

/notes/
/labs/
/runbooks/
/projects/
/assets/        # screenshot/log yang sudah dimasking

```

---

## 0. Setup & Baseline (Lab Legal)
### 0.1 Hardware & OS
- [x] Satu mesin utama (laptop/PC) + ruang disk cukup
- [x] Install virtualisasi: VirtualBox/VMware (pilih 1)
- [x] Siapkan OS host (Windows/macOS/Linux) stable

### 0.2 Lab Environment (pilih 1 atau gabung)
- [x] Docker (wajib bila bisa)
- [ ] VM attacker (Kali/Parrot/Ubuntu)
- [ ] VM target (Ubuntu + apps vulnerable / Metasploitable / Windows eval opsional)
- [ ] Network mode: NAT vs Host-only (paham bedanya)
- [ ] Snapshot VM (before/after)

### 0.3 Tools Wajib (konsep + pemakaian aman)
- [ ] Git
- [ ] Linux CLI (bash)
- [x] Browser DevTools
- [ ] Burp Suite Community (proxy, repeater, intruder basic *untuk lab*)
- [ ] Nmap (discovery & service enumeration)
- [ ] Wireshark/tcpdump (traffic analysis)
- [ ] Python dasar (scripting)
- [ ] Password manager untuk lab (jangan hardcode)

### 0.4 Target Lab Legal (minimal 2)
- [x] OWASP Juice Shop (web)
- [x] DVWA / bWAPP (web)
- [x] WebGoat (training)
- [ ] Local intentionally vulnerable API (buat sendiri) — opsional

### 0.5 Repo Hygiene
- [x] `.gitignore` untuk logs, dumps, secrets
- [x] Rule masking: token/password selalu `****`
- [x] Template catatan & report siap

**Bukti:**
- [x] `labs/00-setup/README.md`:
  - [ ] topologi lab (diagram singkat)
  - [ ] list tools + versi
  - [x] screenshot Docker running (container + halaman lab)
  - [x] cara reset lab (compose down)
  - [ ] issue + solusi
---

## 1. Fundamental Wajib (Komputer, Network, Web)
### 1.1 Linux Fundamentals (untuk security)
- [ ] Filesystem, permission, owner/group, umask
- [ ] Process: ps/top, service, systemd, logs (journalctl)
- [ ] Users/groups, sudoers (konsep)
- [ ] Networking: ip/route, ss/netstat, dns lookup
- [ ] File integrity: hash (sha256), tar/gzip

### 1.2 Networking Fundamentals (inti)
- [ ] OSI/TCP-IP model (fungsi tiap layer)
- [ ] IP/subnet, gateway, NAT
- [ ] DNS, HTTP/HTTPS, TLS (handshake konsep)
- [ ] Ports & sockets, stateful vs stateless
- [ ] Packet capture: filter dasar, follow TCP stream

### 1.3 Web Fundamentals (inti AppSec)
- [ ] Request/response, method, status code
- [ ] Cookies, session, headers penting
- [ ] CORS, SOP, CSRF konsep
- [ ] Encoding: URL/Base64/HTML entities
- [ ] JSON, REST basics

**Bukti:**
- [ ] `labs/01-fundamentals/`:
  - latihan tcpdump/wireshark (pcap + ringkasan)
  - catatan analisis 10 header umum
- [ ] `notes/fundamentals-linux-network-web.md`

---

## 2. Programming untuk Security (Minimal)
### 2.1 Python untuk automasi
- [ ] requests/http client, parsing JSON
- [ ] regex dasar
- [ ] file IO (log)
- [ ] argparse (CLI)
- [ ] error handling (try/except)
- [ ] unit test dasar

### 2.2 Bash untuk operasi
- [ ] pipe, grep/sed/awk basic
- [ ] curl usage (header/body)
- [ ] log parsing sederhana

**Bukti:**
- [ ] `labs/02-scripting/`:
  - `http-checker` (cek endpoint + simpan hasil)
  - `log-analyzer` (hitung error rate sederhana)
- [ ] `notes/scripting.md`

---

## 3. Recon & Enumeration (Aman, Terukur)
> Fokus: discovery permukaan serangan dan pemetaan aset (tanpa eksploit rinci).

### 3.1 Asset Discovery (lab)
- [ ] Identifikasi host aktif (range kecil)
- [ ] Identifikasi port/service yang terbuka
- [ ] Fingerprinting versi (secukupnya)
- [ ] Directory/content discovery konsep
- [ ] Mapping tech stack (server, framework)

### 3.2 Threat Modeling sederhana
- [ ] Asset → entry point → trust boundary
- [ ] STRIDE ringkas (paham kegunaan)
- [ ] Prioritas risiko (impact × likelihood)

**Bukti:**
- [ ] `labs/03-recon/README.md`:
  - tabel aset/port/service
  - diagram alur request
  - “top 5 risk hypothesis”
- [ ] `notes/recon-enum.md`

---

## 4. Web Vulnerabilities (OWASP) — Konsep + Validasi Aman
> Target: paham pola, dampak, dan mitigasi. Latihan di Juice Shop/DVWA/WebGoat.

### 4.1 Injection & Input Handling
- [ ] SQLi konsep (parameterization vs string concat)
- [ ] Command injection konsep
- [ ] Template injection konsep (SSTI)
- [ ] Validasi input vs encoding output

### 4.2 XSS & Browser Security
- [ ] Reflected vs Stored vs DOM XSS
- [ ] CSP konsep
- [ ] Output encoding yang benar (konteks HTML/attr/JS)

### 4.3 Auth & Session
- [ ] Broken auth patterns
- [ ] Session fixation/hijacking konsep
- [ ] Password policy, hashing (bcrypt/argon2)
- [ ] MFA konsep (kapan perlu)

### 4.4 Access Control
- [ ] IDOR/BOLA (object level auth)
- [ ] Horizontal vs vertical privilege escalation konsep
- [ ] RBAC/ABAC konsep + enforcement server-side

### 4.5 CSRF, SSRF, File Upload
- [ ] CSRF token, same-site cookie
- [ ] SSRF konsep (metadata endpoint)
- [ ] Upload: content-type spoofing, path traversal konsep

### 4.6 Security Misconfiguration
- [ ] Debug mode exposure
- [ ] Default credentials
- [ ] Insecure headers
- [ ] Directory listing

### 4.7 Sensitive Data Exposure
- [ ] Secret in repo/log
- [ ] PII masking
- [ ] TLS misconfig dasar

**Bukti:**
- [ ] `labs/04-owasp-web/`:
  - minimal 10 temuan di lab (Info–High) dengan mitigasi
- [ ] `notes/owasp-top10.md`

---

## 5. API Security (Modern Reality)
### 5.1 REST API Core
- [ ] Auth: token vs session
- [ ] Pagination & filtering abuse (konsep)
- [ ] Rate limit, quota, throttling
- [ ] Input validation (schema)
- [ ] Error handling (jangan leak stacktrace)

### 5.2 OWASP API Top 10 (konsep)
- [ ] BOLA/BFLA
- [ ] Excessive data exposure
- [ ] Mass assignment
- [ ] Improper assets management
- [ ] SSRF via API

**Bukti:**
- [ ] `labs/05-api-security/`:
  - audit 1 API lab + report 8 temuan
- [ ] `notes/api-security.md`

---

## 6. Secure Code Review (Praktis)
### 6.1 Code Review Mindset
- [ ] Data flow: input → sink
- [ ] AuthZ enforcement points
- [ ] Secret handling
- [ ] Logging & error boundary

### 6.2 Checklist Review per modul
- [ ] Auth/login/reset
- [ ] File upload
- [ ] Admin panel
- [ ] Payment/order (opsional)

**Bukti:**
- [ ] `runbooks/code-review-checklist.md`
- [ ] `labs/06-code-review/` review repo sample (ringkasan temuan)

---

## 7. Malware/Reverse (Opsional tapi naik level)
- [ ] Dasar file types (PE/ELF), strings, entropy
- [ ] Static analysis ringan
- [ ] Sandbox mindset (VM terisolasi)
- [ ] IOC extraction (konsep)

**Bukti:**
- [ ] `labs/07-reverse-basics/README.md`

---

## 8. Cloud & Container Security (Production)
### 8.1 Docker/Container
- [ ] Image hygiene (base image minimal)
- [ ] Secrets via env vs secret store
- [ ] Least privilege (user non-root)
- [ ] Network isolation konsep

### 8.2 Cloud IAM (konsep)
- [ ] IAM role/policy basic
- [ ] Storage exposure (public bucket)
- [ ] Metadata service risk (konsep)

### 8.3 Kubernetes (opsional)
- [ ] RBAC, namespace isolation
- [ ] Pod security konsep
- [ ] Ingress & TLS

**Bukti:**
- [ ] `labs/08-cloud-container/` audit docker-compose + hardening plan
- [ ] `notes/cloud-container-security.md`

---

## 9. Detection, Logging, Incident Response (Blue Team)
### 9.1 Logging yang benar
- [ ] Audit log (who/what/when)
- [ ] Security events: auth fail, privilege change
- [ ] Log retention & masking

### 9.2 Monitoring & Alerting
- [ ] Threshold vs anomaly (konsep)
- [ ] Alert fatigue mitigation
- [ ] Health check vs security check

### 9.3 Incident Response (IR)
- [ ] Triage: scope, containment, eradication, recovery
- [ ] Evidence handling (hash, timeline)
- [ ] Postmortem & action items

**Bukti:**
- [ ] `runbooks/incident-response.md`
- [ ] `runbooks/logging-standard.md`

---

## 10. Reporting (Skill yang dibayar)
- [ ] Executive summary (bahasa bisnis)
- [ ] Technical detail (repro aman + bukti)
- [ ] Risk rating + prioritas fix
- [ ] Verification steps (before/after)
- [ ] Remediation roadmap (quick win vs long-term)

**Bukti:**
- [ ] `projects/p3-reporting/` 1 laporan lengkap (PDF/MD)

---

# Capstone Projects (Wajib)

## P1 — Build Vulnerable App (Legal, untuk belajar)
- [ ] Buat aplikasi web kecil (login + CRUD)
- [ ] Sengaja tanam 5 kelas bug (tanpa dipublish)
- [ ] Buat “fix branch” untuk semua bug
**Bukti:**
- [ ] `projects/p1-vuln-app/README.md` + diff fix

## P2 — Full Web Pentest Workflow (Lab)
- [ ] Recon → mapping → temuan → mitigasi → verifikasi
- [ ] Minimal 10 temuan, 1 laporan rapi
**Bukti:**
- [ ] `projects/p2-web-pentest/README.md`

## P3 — API Security Audit (Lab)
- [ ] Audit API + auth + rate limit + logging
- [ ] Minimal 8 temuan + rekomendasi
**Bukti:**
- [ ] `projects/p3-api-audit/README.md`

## P4 — Detection & IR Drill
- [ ] Simulasi incident sederhana (login brute force, token leak *di lab*)
- [ ] Buat timeline + containment plan + hardening
**Bukti:**
- [ ] `projects/p4-ir-drill/README.md`

---

# Definition of Done (DoD)
Sebuah item dianggap selesai jika:
- [ ] Bisa dijelaskan ulang (1 paragraf) + contoh dampak
- [ ] Bisa dipraktikkan dari nol di environment baru
- [ ] Ada bukti di repo (`labs/` / `projects/` / `runbooks/`)
- [ ] Bisa menyebutkan minimal 2 mitigasi yang benar
