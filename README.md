# 🏦 SecureBank - Professional Banking Application

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![CustomTkinter](https://img.shields.io/badge/CustomTkinter-5.0+-green.svg)
![SQLite](https://img.shields.io/badge/SQLite-3-orange.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

A modern, feature-rich desktop banking application built with Python and CustomTkinter, featuring a premium UI/UX design and comprehensive banking operations.

[Features](#-features) • [Installation](#-installation) • [Usage](#-usage) • [Screenshots](#-screenshots) • [Documentation](#-documentation)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [How It Works](#-how-it-works)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌟 Overview

**SecureBank** is a professional-grade desktop banking application that provides a complete banking experience with modern UI/UX design. Built with Python and CustomTkinter, it offers secure account management, transaction tracking, and money transfers with an intuitive, card-based interface optimized for dark mode.

### Why SecureBank?

- ✅ **Professional UI** - Premium card-based design with gradients and smooth animations
- ✅ **Complete Banking** - Deposits, withdrawals, transfers, and transaction history
- ✅ **Secure** - PIN-based authentication with SQLite database
- ✅ **User-Friendly** - Intuitive interface with visual feedback and emoji icons
- ✅ **Persistent Data** - All transactions and account data stored securely

---

## ✨ Features

### 🔐 Account Management
- **User Registration** - Create new accounts with unique account numbers
- **Secure Login** - PIN-based authentication system
- **Account Details** - View complete account information including creation date

### 💰 Banking Operations
- **Deposits** - Add money to your account with instant balance updates
- **Withdrawals** - Withdraw money with automatic balance validation
- **Money Transfers** - Send money to other accounts within the system
- **Balance Inquiry** - Real-time balance display with formatted currency

### 📊 Transaction Tracking
- **Complete History** - View all deposits, withdrawals, and transfers
- **Timestamps** - Each transaction logged with date and time
- **Color-Coded** - Visual distinction between income and expenses
- **Detailed Records** - Transaction type, amount, and description for each entry

### 🎨 Modern UI/UX
- **Dark Mode Optimized** - Beautiful dark theme with vibrant accents
- **Card-Based Layout** - Material design-inspired interface
- **Responsive Design** - Smooth scrolling and proper spacing
- **Visual Feedback** - Color-coded actions and emoji icons
- **Gradient Backgrounds** - Premium look and feel

---

## 🛠 Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Language** | Python 3.8+ | Core application logic |
| **GUI Framework** | CustomTkinter 5.0+ | Modern UI components |
| **Database** | SQLite 3 | Data persistence |
| **Standard Libraries** | tkinter, random, datetime | Built-in functionality |

---

## 📦 Installation

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)

### Step-by-Step Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/codedbyamankanojiya/SecureBank.git
   cd SecureBank
   ```

2. **Install Dependencies**
   ```bash
   pip install customtkinter
   ```

3. **Run the Application**
   ```bash
   python SecureBank.py
   ```

### Alternative: Virtual Environment (Recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install customtkinter

# Run application
python SecureBank.py
```

---

## 🚀 Usage

### First Time Setup

1. **Launch the Application**
   ```bash
   python SecureBank.py
   ```

2. **Create an Account**
   - Click "Create New Account" on the login screen
   - Enter your full name
   - Create a 4-digit PIN
   - **Important:** Save the account number displayed in the success message!

3. **Login**
   - Enter your account number
   - Enter your 4-digit PIN
   - Click "Sign In"

### Daily Operations

#### Making a Deposit
1. Navigate to the Dashboard
2. In the "Deposit Money" card, enter the amount
3. Click "Deposit"
4. View updated balance instantly

#### Making a Withdrawal
1. Navigate to the Dashboard
2. In the "Withdraw Money" card, enter the amount
3. Click "Withdraw"
4. System validates sufficient balance before processing

#### Transferring Money
1. Click "Go to Transfer" on the Dashboard
2. Enter recipient's account number
3. Enter transfer amount
4. Click "Transfer Now"
5. Both accounts updated instantly

#### Viewing Transaction History
1. Click "📊 Transaction History" from Dashboard
2. Scroll through all transactions
3. View details: type, amount, timestamp, description

#### Checking Account Details
1. Click "👤 Account Details" from Dashboard
2. View account holder name, account number, balance, and creation date

---

## 📁 Project Structure

```
SecureBank/
│
├── SecureBank.py            # Main application file
├── bank.db                 # SQLite database (auto-generated)
├── README.md               # This file
├── LICENSE                 # MIT License
└── .gitattributes         # Git configuration
```

### Code Architecture

```
SecureBank.py
│
├── DatabaseManager         # Database operations layer
│   ├── create_tables()    # Initialize database schema
│   ├── create_user()      # User registration
│   ├── get_user_by_account() # User retrieval
│   ├── update_balance()   # Balance updates
│   ├── add_transaction()  # Transaction logging
│   ├── get_transaction_history() # Retrieve transactions
│   └── transfer_money()   # Inter-account transfers
│
├── BankController          # Business logic layer
│   ├── sign_up()          # Registration logic
│   ├── sign_in()          # Authentication
│   ├── deposit()          # Deposit processing
│   ├── withdraw()         # Withdrawal processing
│   ├── transfer()         # Transfer processing
│   ├── get_transaction_history() # History retrieval
│   └── get_account_info() # Account information
│
└── GUI Components          # User interface layer
    ├── BankApp            # Main application window
    ├── LoginFrame         # Login screen
    ├── RegisterFrame      # Registration screen
    ├── DashboardFrame     # Main dashboard
    ├── TransactionHistoryFrame # Transaction list
    ├── TransferFrame      # Money transfer screen
    └── AccountDetailsFrame # Account information display
```

---

## ⚙️ How It Works

### Database Schema

#### Users Table
```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    pin TEXT NOT NULL,
    account_number TEXT UNIQUE NOT NULL,
    balance INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
)
```

#### Transactions Table
```sql
CREATE TABLE transactions (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER NOT NULL,
    type TEXT NOT NULL,
    amount INTEGER NOT NULL,
    recipient_account TEXT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    description TEXT,
    FOREIGN KEY (user_id) REFERENCES users(id)
)
```

### Transaction Flow

#### Deposit Process
1. User enters amount in deposit field
2. `BankController.deposit()` validates input
3. Balance updated in database via `DatabaseManager.update_balance()`
4. Transaction logged via `DatabaseManager.add_transaction()`
5. UI refreshes to show new balance

#### Transfer Process
1. User enters recipient account and amount
2. `BankController.transfer()` validates both accounts exist
3. `DatabaseManager.transfer_money()` executes:
   - Validates sender has sufficient balance
   - Deducts from sender's balance
   - Adds to recipient's balance
   - Logs transaction for both users (TRANSFER_OUT and TRANSFER_IN)
4. Success message displayed

### Security Features

- **PIN Authentication** - 4-digit PIN required for login
- **Account Validation** - Checks account existence before operations
- **Balance Verification** - Prevents overdrafts
- **Self-Transfer Prevention** - Cannot transfer to own account
- **Database Integrity** - Foreign key constraints ensure data consistency

---

## 🎨 Screenshots

### Login Screen
Modern centered card design with gradient background and smooth animations.

### Dashboard
Card-based layout with balance display and quick action cards for deposits, withdrawals, and transfers.

### Transaction History
Scrollable list with color-coded transactions, icons, and detailed information.

### Transfer Money
Clean interface for sending money to other accounts with validation.

### Account Details
Professional display of all account information in organized cards.

---

## 🎨 Design System

### Color Palette

| Color | Hex Code | Usage |
|-------|----------|-------|
| Primary Blue | `#1E88E5` | Login, Dashboard header, primary actions |
| Success Green | `#43A047` | Deposits, positive transactions |
| Warning Red | `#E53935` | Withdrawals, negative transactions |
| Accent Orange | `#FB8C00` | Transfers, highlights |
| Info Purple | `#5E35B1` | Transaction history |
| Teal | `#00897B` | Account details |

### Typography

- **Headers:** 28-36px, Bold
- **Subheaders:** 18-20px, Regular
- **Body Text:** 14-16px, Regular
- **Small Text:** 11-12px, Regular

---

## 🔮 Future Enhancements

- [ ] Profile picture upload
- [ ] Email notifications for transactions
- [ ] Transaction filters (date range, type)
- [ ] Export transaction history to PDF/CSV
- [ ] Recurring transfers/scheduled payments
- [ ] Two-factor authentication (2FA)
- [ ] Multi-currency support
- [ ] Account statements generation
- [ ] Password recovery system
- [ ] Admin dashboard for management

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Follow PEP 8 style guide for Python code
- Add comments for complex logic
- Test all features before submitting PR
- Update README if adding new features

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Aman Kanojiya**
- GitHub: [@codedbyamankanojiya](https://github.com/codedbyamankanojiya)


---

## 🙏 Acknowledgments

- [CustomTkinter](https://github.com/TomSchimansky/CustomTkinter) - Modern UI framework
- Python Community - For excellent documentation and support
- Material Design - For design inspiration

---

## 📞 Support

If you encounter any issues or have questions:

1. Check the [Issues](https://github.com/codedbyamankanojiya/SecureBank/issues) page
2. Create a new issue with detailed description


---

<div align="center">

**Made with ❤️ using Python and CustomTkinter By Aman Kanojiya**

⭐ Star this repository if you found it helpful!

</div>
