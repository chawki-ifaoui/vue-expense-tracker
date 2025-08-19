# Vue Expense Tracker

A modern, responsive expense tracking application built with Vue 3, Vite, and Vuetify. This application helps users manage their personal finances by tracking income and expenses with a beautiful, intuitive interface featuring Material Design components. Optimized for both desktop and mobile devices with PWA capabilities and comprehensive date tracking.

## 🚀 Features

- **Add Transactions**: Easily add income (positive amounts) and expenses (negative amounts)
- **Date Tracking**: Add dates to all transactions with a beautiful date picker
- **Real-time Balance**: View your current balance updated in real-time
- **Income/Expense Summary**: See total income and expenses at a glance with beautiful cards
- **Transaction History**: View all your transactions in a modern list format with dates and icons
- **Date Filtering**: Filter transactions by date ranges (Today, Yesterday, This Week, This Month, etc.)
- **Smart Date Display**: Intelligent date formatting (Today, Yesterday, Weekday names, etc.)
- **Delete Transactions**: Remove unwanted transactions with a single click
- **Local Storage**: All data is automatically saved to your browser's local storage
- **Toast Notifications**: Get instant feedback when adding or deleting transactions
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices
- **Mobile Optimized**: Touch-friendly interface with optimized layouts for mobile
- **PWA Ready**: Progressive Web App capabilities for mobile installation
- **Modern UI/UX**: Beautiful Material Design interface with smooth animations
- **Form Validation**: Real-time validation with helpful error messages

## 🛠️ Technology Stack

- **Frontend Framework**: Vue 3 (Composition API)
- **Build Tool**: Vite
- **UI Framework**: Vuetify 3 (Material Design)
- **Icons**: Material Design Icons (MDI)
- **Styling**: Vuetify + Custom CSS
- **Notifications**: Vue Toastification
- **Data Persistence**: Local Storage
- **Mobile Optimization**: Responsive design with PWA support
- **Date Handling**: Native JavaScript Date API with intelligent formatting

## 🎨 Design Features

- **Material Design**: Modern, clean interface following Google's Material Design principles
- **Gradient Backgrounds**: Beautiful gradient app bar and background
- **Color-coded Elements**: Visual distinction between income (green) and expenses (red)
- **Smooth Animations**: Hover effects, transitions, and loading states
- **Responsive Cards**: Modern card-based layout with proper elevation
- **Typography**: Inter font for excellent readability
- **Icons**: Meaningful icons throughout the interface for better UX
- **Mobile-First Design**: Optimized for mobile devices with touch-friendly elements
- **Date Picker**: Beautiful modal date picker for transaction dates

## 📱 Mobile Features

- **Touch-Friendly Interface**: All buttons and interactive elements sized for touch
- **Responsive Layout**: Adapts perfectly to different screen sizes
- **Mobile Navigation**: Optimized app bar and navigation for mobile
- **Form Optimization**: Mobile-optimized form fields with proper keyboard handling
- **PWA Support**: Can be installed as a mobile app on supported devices
- **Landscape Mode**: Optimized layout for landscape orientation
- **High DPI Support**: Crisp graphics on high-resolution displays
- **Mobile Date Picker**: Touch-friendly date selection on mobile devices

## 📅 Date Features

- **Transaction Dating**: Add dates to all transactions with a user-friendly date picker
- **Smart Date Display**: Intelligent date formatting that shows "Today", "Yesterday", or weekday names
- **Date Filtering**: Filter transactions by various date ranges:
  - All Time
  - Today
  - Yesterday
  - This Week
  - This Month
  - Last 30 Days
  - Custom Range
- **Date-based Sorting**: Transactions automatically sorted by date (newest first)
- **Date Range Summary**: Income/Expense cards show the date range of displayed transactions
- **Backward Compatibility**: Existing transactions without dates are automatically assigned today's date

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

## 📱 Mobile Installation

The app can be installed as a Progressive Web App (PWA) on mobile devices:

### **iOS (Safari)**
1. Open the app in Safari
2. Tap the Share button (square with arrow)
3. Select "Add to Home Screen"
4. Tap "Add"

### **Android (Chrome)**
1. Open the app in Chrome
2. Tap the menu (three dots)
3. Select "Add to Home screen"
4. Tap "Add"

## 🚀 Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build

## 💡 Usage

### Adding a Transaction
1. Enter a description in the "Transaction Description" field
2. Enter the amount:
   - **Positive numbers** for income (e.g., 500)
   - **Negative numbers** for expenses (e.g., -50)
3. Click on the "Date" field to select a transaction date (defaults to today)
4. Click "Add Transaction" button

### Managing Transactions
- View your current balance in the prominent card at the top
- See total income and expenses in the color-coded summary cards with date range
- Use the date filter to view transactions from specific time periods
- Scroll through your transaction history with dates and visual indicators
- Click the delete icon to remove any transaction

### Date Filtering
- Use the "Filter by Date" dropdown to view transactions from different time periods
- Choose from predefined ranges like "Today", "This Week", "This Month"
- View "All Time" to see all transactions
- Transactions are automatically sorted by date (newest first)

### Data Persistence
- All transactions are automatically saved to your browser's local storage
- Your data persists between browser sessions
- No account creation required

## 📁 Project Structure

```
vue-expense-tracker/
├── src/
│   ├── components/
│   │   ├── AddTransaction.vue    # Modern form with date picker and Vuetify components
│   │   ├── Balance.vue          # Balance display with Material Design card
│   │   ├── Header.vue           # Gradient app bar with wallet icon
│   │   ├── IncomeExpenses.vue   # Income/expense cards with date range display
│   │   └── TransactionList.vue  # Modern list with dates, filtering, and actions
│   ├── assets/
│   │   └── style.css           # Custom styles and mobile optimizations
│   ├── App.vue                 # Main application with Vuetify layout and date handling
│   └── main.js                # Vuetify configuration and app setup
├── public/                    # Static assets
├── index.html                # HTML template with PWA meta tags
└── package.json              # Project dependencies
```

## 🎨 Key Components

- **App.vue**: Main application with Vuetify layout, state management, date handling, and data persistence
- **AddTransaction.vue**: Modern form with Vuetify text fields, date picker, validation, and loading states
- **Balance.vue**: Material Design card displaying current total balance
- **IncomeExpenses.vue**: Color-coded cards showing income and expense summaries with date range information
- **TransactionList.vue**: Modern list with dates, filtering, avatars, icons, and delete functionality
- **Header.vue**: Beautiful gradient app bar with wallet icon and typography

## 🎨 Vuetify Styling

The application uses Vuetify 3 for a modern Material Design interface:

### **Theme Configuration**
- Custom color palette with primary, success, and error colors
- Light theme with consistent color scheme
- Material Design Icons integration

### **Component Styling**
- **Cards**: Elevated cards with hover effects and proper spacing
- **Buttons**: Modern buttons with icons and loading states
- **Text Fields**: Outlined fields with validation and icons
- **Lists**: Clean list items with avatars and action buttons
- **App Bar**: Gradient background with professional typography
- **Date Picker**: Beautiful modal date picker with calendar interface

### **Mobile Optimizations**
- **Responsive Grid**: Vuetify's responsive grid system for all screen sizes
- **Touch Targets**: All interactive elements sized for touch (44px minimum)
- **Mobile Typography**: Responsive text sizing for different screen sizes
- **Form Optimization**: Mobile-optimized form fields with proper keyboard handling
- **Landscape Support**: Optimized layouts for landscape orientation
- **Mobile Date Picker**: Touch-friendly date selection interface

### **Custom Enhancements**
- Smooth transitions and hover animations
- Custom scrollbar styling
- Responsive typography adjustments
- Gradient backgrounds and modern color schemes
- Mobile-specific CSS optimizations
- Intelligent date formatting and display

## 🔧 Customization

The application uses Vuetify for styling with custom CSS enhancements. You can customize the appearance by:

1. **Modifying Vuetify theme** in `src/main.js`
2. **Updating component styles** in individual Vue files
3. **Customizing global styles** in `src/assets/style.css`
4. **Adjusting mobile breakpoints** in the CSS media queries
5. **Customizing date formatting** in the date utility functions

## 📱 Browser Support

This application works in all modern browsers that support:
- ES6+ JavaScript
- CSS Grid and Flexbox
- Local Storage API
- Material Design Icons
- Progressive Web App features
- Date API and formatting

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
- Styled with [Vuetify 3](https://vuetifyjs.com/) (Material Design)
- Icons from [Material Design Icons](https://materialdesignicons.com/)
- Toast notifications powered by [Vue Toastification](https://github.com/Maronato/vue-toastification)
