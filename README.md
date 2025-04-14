## README: Income and Expenses Tracker

The **Income and Expenses Tracker** is a web-based application that allows users to manage their monthly income, expenses, and grocery purchases. Built with HTML, CSS, JavaScript, and Bootstrap, it provides a user-friendly interface to track financial data and view a yearly summary. All data is stored locally on the user's device using the browser's `localStorage`, ensuring privacy with no server-side storage.

### **Application Files**

The application consists of three main HTML files, each serving a distinct purpose:

1. **`index.html` - Home Page**
   - **Purpose**: The entry point where users select a month to manage or view a yearly summary.
   - **Features**:
     - Displays a list of buttons for each month (January to December).
     - Includes a "Summary" button to view aggregated financial data.
   - **Navigation**:
     - Clicking a month links to `month.html?month=<month_code>` (e.g., `month.html?month=jan`).
     - The "Summary" button links to `summary.html`.

2. **`month.html` - Monthly Financial Management**
   - **Purpose**: Allows users to add, edit, and delete financial entries for a specific month.
   - **Features**:
     - **Income Section**: Add and delete income amounts (e.g., salary).
     - **Expenses Section**: Add expenses with details like description, main category (e.g., Housing), sub-category (e.g., Rent), and amount.
     - **Groceries Section**: Track grocery purchases with description, quantity, and amount.
     - **Real-Time Totals**: A fixed panel shows total income, expenses (including groceries), and balance (income - expenses).
     - **Back Button**: Returns to `index.html`.
   - **Dynamic Display**: The page title reflects the selected month (e.g., "March") based on the URL query parameter.

3. **`summary.html` - Yearly Financial Overview**
   - **Purpose**: Displays a table summarizing financial data for all months.
   - **Features**:
     - Shows columns for Month, Income, Expense (including groceries), and Balance.
     - Aggregates data from all months to provide a yearly snapshot.
     - Includes a "Back" button to return to `index.html`.

### **How Items Are Saved**

- **Local Storage Mechanism**:
  - The application uses the browser's `localStorage` to save all financial data directly on the user's device. No data is sent to or stored on any server, ensuring privacy and offline functionality.
  - Each month's data is stored under a unique key in the format `budget_<month_code>` (e.g., `budget_jan` for January).
  - **Data Structure**:
    - **Income**: Stored as an array of numbers (e.g., `[1000, 2000]` for two income entries).
    - **Expenses**: Stored as an array of objects with fields like `description`, `mainCategory`, `subCategory`, and `amount` (e.g., `[{description: "Rent", amount: 1500, ...}]`).
    - **Groceries**: Stored as an array of objects with `description`, `quantity`, and `amount` (e.g., `[{description: "Milk", quantity: 2, amount: 100}]`).
  - Example `localStorage` entry for January:
    ```json
    {
      "budget_jan": {
        "incomeList": [5000, 2000],
        "expenseList": [{"description": "Rent", "mainCategory": "Housing", "subCategory": "Rent/Mortgage", "amount": 2000}],
        "groceryList": [{"description": "Milk", "quantity": 2, "amount": 100}]
      }
    }
  - **Saving Process**:
    - In `month.html`, whenever a user adds, edits, or deletes an income, expense, or grocery entry, the data is updated in memory and immediately saved to `localStorage` using `localStorage.setItem()`.
    - Example: Adding an income triggers:
      ```javascript
      incomeList.push(incomeAmount);
      saveData(); // Calls localStorage.setItem(`budget_${currentMonth}`, JSON.stringify(data));
      ```
  - **Loading Process**:
    - When `month.html` loads, it retrieves the saved data for the current month using `localStorage.getItem(`budget_${currentMonth}`)`.
    - `summary.html` loops through all months, reading each `budget_<month>` key to populate the summary table.
  - **Persistence**:
    - Data remains in `localStorage` until the user clears their browser data or the application explicitly removes it (no such feature is currently implemented).
    - Users can access their data across sessions on the same device and browser.

- **No Server Storage**:
  - Since all data is stored in `localStorage`, nothing is transmitted over the internet or saved on a server.
  - This makes the application fully client-side, ideal for offline use and privacy-conscious users.
  - Note: Data is tied to the specific browser and device. If the user switches devices or clears their browser storage, the data will not be accessible unless exported (export functionality is not currently implemented).

### **Key Features**
- **User-Friendly Interface**: Dark-themed, responsive design using Bootstrap 5.3 for accessibility on mobile and desktop.
- **Real-Time Updates**: Totals and balances update instantly as users modify entries.
- **Category Management**: Predefined expense categories (e.g., Housing, Food) with sub-categories for detailed tracking.
- **Privacy-Focused**: Local storage ensures financial data stays on the user’s device.
- **Yearly Summary**: Aggregates monthly data for a comprehensive financial overview.

### **Usage Instructions**
1. Open `index.html` in a web browser.
2. Click a month to manage its finances in `month.html`.
3. Add income, expenses, or groceries; data saves automatically to your browser.
4. Return to `index.html` and click "Summary" to view the yearly overview in `summary.html`.
5. All data is stored locally and persists until you clear your browser’s storage.

### **Limitations**
- Data is device- and browser-specific; no cloud backup or cross-device sync.
- `localStorage` has a size limit (typically 5-10 MB), which may restrict extensive data entry.
- No export/import feature to back up or transfer data (future enhancement suggested).

### **Development Notes**
- **Dependencies**: Bootstrap 5.3 (via CDN) for styling and JavaScript components.
- **Storage**: Uses `localStorage` with keys like `budget_jan`, `budget_feb`, etc.
- **Future Improvements**:
  - Add data export/import for backups.
  - Implement a "Clear Data" option.
  - Include charts for visualizing financial trends.
  - Enhance validation to prevent invalid entries.

---
