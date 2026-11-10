# LogDetective 

**LogDetective** is a high-performance cybersecurity web dashboard designed to ingest, parse, and analyze massive raw server access logs (Nginx/Apache) in real-time. By leveraging zero-allocation C# parsing techniques (`ReadOnlySpan<char>`), it translates millions of raw log entries into actionable visual threat intelligence without exhausting server memory.

---

## Key Features

- **High-Performance Parsing:** Zero-allocation stream parsing to process multi-gigabyte log files rapidly with minimal memory footprint.
- **Automated Threat Detection:** Built-in rules to detect anomalous traffic, including:
  - **SQL Injection (SQLi)** payloads in request URLs
  - **Cross-Site Scripting (XSS)** pattern detection
  - **Brute-Force Attacks** (aggregated `401 Unauthorized` spikes per IP)
- **Real-Time Telemetry:** Live progress streaming and dynamic metrics via **SignalR** WebSockets.
- **Batch Processing & Storage:** Asynchronous file streaming and bulk database inserts using `EFCore.BulkExtensions`.
- **Interactive Visualizations:** Time-series charts and detailed threat tables for security analysts.

---

## Architecture & Processing Flow

1. **Ingestion:** Security Analyst uploads raw log files (`.log`, `.txt`) through the web portal.
2. **Asynchronous Handoff:** ASP.NET Core API delegates processing to a background worker (`IHostedService`).
3. **High-Speed Parsing:** Stream chunks are parsed using C# `ReadOnlySpan<char>` for ultra-fast, low-allocation extraction.
4. **Threat Evaluation & Batch Storage:** Parsed logs are evaluated against detection rules and written in bulk to the database.
5. **Telemetry & Dashboard:** Real-time stats are pushed to the interactive React dashboard via SignalR.

---

## 🛠️ Tech Stack

| Domain | Technology |
| :--- | :--- |
| **Backend & API** | C# / ASP.NET Core Web API |
| **Performance Engine** | `ReadOnlySpan<T>`, `Memory<T>`, `StreamReader` |
| **Real-Time Communication** | ASP.NET Core SignalR |
| **ORM & Database** | Entity Framework Core + `EFCore.BulkExtensions` (SQL Server / PostgreSQL) |
| **Frontend UI** | React / HTML / CSS / JavaScript |
| **Data Visualization** | Chart.js / ApexCharts |

---

## 🚦 Getting Started

### Prerequisites

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download) or later
- [Node.js](https://nodejs.org/) (v18+)
- [SQL Server](https://www.microsoft.com/sql-server) or [PostgreSQL](https://www.postgresql.org/)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/ArbazNiaz/LogDetective.git
   cd LogDetective
   ```

2. **Setup Backend:**
   ```bash
   cd src/LogDetective.API
   dotnet restore
   dotnet run
   ```

3. **Setup Frontend:**
   ```bash
   cd src/LogDetective.UI
   npm install
   npm start
   ```

---

## License

This project is open-source and available under the [MIT License](LICENSE).
