# 📡 OfflineUPI — UPI Without Internet

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-17%2B-ED8B00?style=flat-square&logo=java&logoColor=white)](https://www.java.com)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.3.5-6DB33F?style=flat-square&logo=spring&logoColor=white)](https://spring.io/projects/spring-boot)

**🌟 Live Demo:** [View Live App](https://huggingface.co/spaces/alwaysprince05e/UPI-Without-Internet)

> A proof-of-concept Spring Boot application demonstrating how digital payments
> (similar to UPI) can work securely **without internet connectivity** using mesh
> network concepts and deferred settlement.

---

## 👨‍💻 Author

**Adarsh**
Dayananda Sagar College of Engineering, Bengaluru

---

## 💡 About the Project

OfflineUPI solves a real-world problem — what happens when you need to make a
UPI payment but have no internet? This project simulates secure offline
transactions using mesh networking (Bluetooth Low Energy, Wi-Fi Direct, Local
LAN) and deferred asynchronous settlement, where encrypted payments sync with
the bank once connectivity is restored.

---

## 🚀 Key Features

- **Mesh Packet Construction** — Compiles transactions into lightweight, signed
  JSON payloads suitable for BLE/offline transport
- **Hybrid Cryptography** — RSA-2048 for secure key exchange + AES-256 for fast
  payload encryption, ensuring only the final banking server can decrypt
- **Idempotency & Concurrency** — Duplicate mesh packets are rejected smoothly;
  concurrent settlements are strictly locked to prevent double-spending
- **Interactive Dashboard** — Dynamic web-based dashboard simulating the
  lifecycle of devices and offline packet relays

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Backend | Java 17, Spring Boot 3.3.5 |
| Database | H2 (In-Memory) + Spring Data JPA |
| Frontend | HTML, CSS, JavaScript |
| Build Tool | Maven |
| Deployment | Docker, HuggingFace Spaces |

---

## 🏗 Architecture

1. **Offline Phase** — Sender initiates a transaction. Details are bundled,
   encrypted via RSA public key (AES key exchange), and signed by the sender.
2. **Mesh Relay Phase** — The encrypted payload (`MeshPacket`) is passed between
   intermediate devices. Devices only forward the blob — they can't read it.
3. **Settlement Phase** — Once internet is available, the packet is pushed to
   `/api/bridge/ingest`. Server decrypts, verifies signature, checks
   idempotency, locks accounts, and settles funds.

---

## 📦 Running Locally

**Prerequisites:** Java 17+ installed

```bash
# Clone the repository
git clone https://github.com/adarshdeshp/OfflineUPI.git
cd OfflineUPI

# Run on Mac/Linux
chmod +x mvnw
./mvnw spring-boot:run

# Run on Windows
.\mvnw.cmd spring-boot:run
```

Open your browser at `http://localhost:8080`

---

## 📄 License

This project is licensed under the MIT License.