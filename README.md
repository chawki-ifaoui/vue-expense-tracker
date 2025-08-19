# Vue Expense Tracker

A modern, responsive expense tracking application built with Vue 3 and Vite. This application helps users manage their personal finances by tracking income and expenses with a clean, intuitive interface.

## 🚀 Features

- **Add Transactions**: Easily add income (positive amounts) and expenses (negative amounts)
- **Real-time Balance**: View your current balance updated in real-time
- **Income/Expense Summary**: See total income and expenses at a glance
- **Transaction History**: View all your transactions in a clean list format
- **Delete Transactions**: Remove unwanted transactions with a single click
- **Local Storage**: All data is automatically saved to your browser's local storage
- **Toast Notifications**: Get instant feedback when adding or deleting transactions
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices

## 🛠️ Technology Stack

- **Frontend Framework**: Vue 3 (Composition API)
- **Build Tool**: Vite
- **Styling**: CSS3
- **Notifications**: Vue Toastification
- **Data Persistence**: Local Storage

## 📦 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd vue-expense-tracker
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**
   Navigate to `http://localhost:5173` to view the application

## 🚀 Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build

## 💡 Usage

### Adding a Transaction
1. Enter a description in the "Text" field
2. Enter the amount:
   - **Positive numbers** for income (e.g., 500)
   - **Negative numbers** for expenses (e.g., -50)
3. Click "Add transaction"

### Managing Transactions
- View your current balance at the top
- See total income and expenses in the summary cards
- Scroll through your transaction history
- Click the "X" button to delete any transaction

### Data Persistence
- All transactions are automatically saved to your browser's local storage
- Your data persists between browser sessions
- No account creation required

## 📁 Project Structure

```
vue-expense-tracker/
├── src/
│   ├── components/
│   │   ├── AddTransaction.vue    # Form to add new transactions
│   │   ├── Balance.vue          # Display current balance
│   │   ├── Header.vue           # Application header
│   │   ├── IncomeExpenses.vue   # Income/expense summary cards
│   │   └── TransactionList.vue  # List of all transactions
│   ├── assets/
│   │   └── style.css           # Global styles
│   ├── App.vue                 # Main application component
│   └── main.js                # Application entry point
├── public/                    # Static assets
├── index.html                # HTML template
└── package.json              # Project dependencies
```

## 🎨 Key Components

- **App.vue**: Main application logic, state management, and data persistence
- **AddTransaction.vue**: Form component for adding new transactions
- **Balance.vue**: Displays the current total balance
- **IncomeExpenses.vue**: Shows income and expense summaries
- **TransactionList.vue**: Renders the list of all transactions with delete functionality

## 🔧 Customization

The application uses CSS for styling. You can customize the appearance by modifying the styles in `src/assets/style.css` and component-specific styles.

## 📱 Browser Support

This application works in all modern browsers that support:
- ES6+ JavaScript
- CSS Grid and Flexbox
- Local Storage API

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- Built with [Vue 3](https://vuejs.org/)
- Styled with modern CSS
- Toast notifications powered by [Vue Toastification](https://github.com/Maronato/vue-toastification)
# vue-expense-tracker
