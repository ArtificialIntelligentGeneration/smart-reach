# TGFlow: High-Load Telegram Outreach Automation

**TGFlow** is an advanced, asynchronous Python application designed for managing large-scale outreach campaigns on Telegram. It leverages the MTProto protocol (via Pyrogram) to handle multiple accounts simultaneously with high performance and human-like behavior simulation.

> **Note:** This project demonstrates advanced usage of `asyncio`, `PyQt6`, and anti-flood algorithms. It is intended for educational purposes and as a portfolio showcase of automation capabilities.

## 🚀 Key Features

*   **Asynchronous Core**: Built on top of `asyncio` and `Pyrogram` (MTProto), allowing concurrent operations across dozens of accounts without blocking the UI.
*   **Intelligent Queue Management**:
    *   **Worker Pool Pattern**: Efficiently distributes tasks (message sending) across available accounts.
    *   **Rate Limiting**: Custom `AntiSpamManager` handles Telegram's flood limits dynamically.
    *   **PeerFlood Detection**: Automatically pauses accounts that receive temporary restrictions and switches to healthy ones.
*   **Human Simulation**:
    *   Randomized delays and "typing" states.
    *   Markdown V2 parsing with HTML input support.
*   **Modern UI**: Responsive interface built with `PyQt6` (Model-View-Controller pattern).
*   **Local Privacy**: All sensitive data (session keys, logs) is stored locally on the user's machine (encrypted by the OS), ensuring data sovereignty.

## 🛠 Tech Stack

*   **Language**: Python 3.10+
*   **Telegram Protocol**: [Pyrogram](https://github.com/pyrogram/pyrogram) (MTProto API)
*   **GUI Framework**: PyQt6 (Qt 6.6)
*   **Concurrency**: `asyncio`, `nest_asyncio`
*   **Data Storage**: SQLite (for state management) + JSON
*   **Utilities**: `BeautifulSoup4` (HTML parsing), `Pillow` (Image optimization)

## 🏗 Architecture Highlights

### The Anti-Flood System (`antispam_manager.py`)
One of the most complex parts of Telegram automation is avoiding bans. TGFlow implements a multi-layer protection system:
1.  **Token Bucket Algorithm**: Controls the rate of outgoing requests.
2.  **Adaptive Backoff**: If an account hits a `FloodWait` error, the system automatically parses the required wait time, pauses the account, and re-schedules the task.
3.  **SpamBot Integration**: (Optional) Automated interaction with `@SpamBot` to check account status and appeal restrictions.

### Multi-Account Orchestration
The application treats accounts as resources in a pool. When a broadcasting campaign starts:
1.  The `BroadcastManager` creates an async task queue.
2.  Available accounts consume tasks from the queue.
3.  If an account dies (ban/logout), it is removed from the pool, and its tasks are re-queued for other accounts.

## 📦 Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ArtificialIntelligentGeneration/smart-reach.git
    cd smart-reach
    ```

2.  **Create a virtual environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Run the application:**
    ```bash
    python main.py
    ```

## 🔒 Configuration

The application stores user data (sessions, logs) in the standard OS user data directory:
*   **Windows**: `%APPDATA%\TGFlow`
*   **macOS**: `~/Library/Application Support/TGFlow`
*   **Linux**: `~/.local/share/TGFlow`

To add accounts, you will need your `api_id` and `api_hash` from [my.telegram.org](https://my.telegram.org).

## 📄 License

This code is provided for portfolio demonstration purposes.
Copyright © 2025. All Rights Reserved.

---
*Built with ❤️ by AiGen - Python & AI Automation Engineer*