# 💬 Quotify — Your Daily Dose (QuoteManagement)

A lightweight **Spring Boot REST API** that fetches an inspirational quote once a day from the **ZenQuotes API**, caches it locally for the day, and serves it back on request — your daily dose of motivation, one API call away. ✨

---

## 📌 What is this project?

**Quotify** is a small Spring Boot backend service with a single job: give you **one fresh quote per day**. The first time you hit its endpoint on a given day, it fetches a random quote from the public **ZenQuotes API**, saves it to a local file along with today's date, and returns it. Any further requests **on the same day** are served instantly from that saved copy instead of calling the external API again — a simple, file-based daily caching mechanism.

---

## ✨ Features / Functionality

- 🌐 **`GET /daily-quote`** endpoint — returns today's quote
- 🔄 **Auto-fetch from ZenQuotes API** (`https://zenquotes.io/api/random`) when no quote has been saved for today
- 💾 **Simple file-based caching** — quote + date are persisted in `daily_quote.txt` (format: `YYYY-MM-DD;quote text`)
- 📅 **Date-aware logic** — if the stored quote's date matches today, it's reused; otherwise a new one is fetched
- 🪶 **No database required** — the `DataSourceAutoConfiguration` is explicitly excluded, keeping the app lightweight and dependency-free for persistence
- ⚡ Built as a minimal **REST microservice**, easy to extend (e.g., add scheduling, a database, or a frontend)

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Language** | ☕ Java 17 |
| **Framework** | 🍃 Spring Boot 3.2.1 |
| **Web Layer** | Spring MVC / REST (`spring-boot-starter-web`) |
| **HTTP Client** | `RestTemplate` (used to call the external ZenQuotes API) |
| **External API** | 🌐 [ZenQuotes API](https://zenquotes.io/) — source of daily quotes |
| **Persistence** | 📄 Plain text file (`daily_quote.txt`) — no database used |
| **Data Layer Dependency** | Spring Data JPA included in `pom.xml`, but its auto-configured datasource is disabled (no DB is actually wired up) |
| **Build Tool** | 🏗️ Maven (`mvnw` wrapper included) |
| **Testing** | JUnit + Spring Boot Test |

### 📁 Project Structure
```
QuoteManagement/
├── src/main/java/com/quote/
│   ├── controller/
│   │   └── QuoteController.java      # Exposes GET /daily-quote, fetches & parses ZenQuotes API
│   ├── service/
│   │   └── DailyQuoteManager.java    # Reads/writes daily_quote.txt for caching
│   └── QuoteManagementApplication.java  # Main entry point (DataSource auto-config excluded)
├── src/main/resources/
│   └── application.properties        # Server port + ZenQuotes API URL
├── daily_quote.txt                   # Local cache file (date;quote)
└── pom.xml
```

---

## 🚀 How to Run

### ✅ Prerequisites
- ☕ **Java 17 (JDK)**
- 🌍 An active **internet connection** (needed to call the ZenQuotes API when fetching a new quote)
- 🏗️ Maven (optional — the `mvnw` wrapper is included, no local Maven install required)

### 1️⃣ Clone the repository
```bash
git clone https://github.com/ParasJain12/Quotify-Your-Daily-Dose.git
cd Quotify-Your-Daily-Dose/QuoteManagement
```

### 2️⃣ Run the application

Using the Maven wrapper (recommended):
```bash
# macOS/Linux
./mvnw spring-boot:run

# Windows
mvnw.cmd spring-boot:run
```

Or build a JAR and run it:
```bash
./mvnw clean package
java -jar target/QuoteManagement-0.0.1-SNAPSHOT.jar
```

### 3️⃣ Get your daily quote 🎉
The app runs on **port 8080** by default (configurable in `application.properties`). Open your browser, or use `curl`:
```bash
curl http://localhost:8080/daily-quote
```

**Example response:**
```
Today's daily quote: The journey, not the destination matters.
```

The first call each day fetches a new quote from ZenQuotes and saves it; every subsequent call that same day returns the cached one instantly. 🔁

---
## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 📬 Contact

For any queries, reach out at **parasjain8103@gmail.com** or use the [Contact Us](https://parasjain12.github.io/) page on the website.

---

<p align="center">Made with ❤️ by Paras Jain</p>
