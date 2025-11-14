# RPA Solution: Dispatcher & Performer (REFramework-Based)

## 📌 Overview

This RPA solution consists of two distinct UiPath projects — **RPA_Dispatcher** and **RPA_Performer** — designed to work together using the **Robotic Enterprise Framework (REFramework)** and **Orchestrator Queues**.

---

## 🧱 Architecture

### 📸 Project Structure Overview
![Project Screenshot](https://github.com/Renish-R/Robotic_Process_Automation_Using_UiPath/blob/main/project.png)

### 1. 🔄 Dispatcher (`RPA_Dispatcher`)
The **Dispatcher** is responsible for reading data from an external source (e.g., Excel or web) and uploading it as transaction items into a **UiPath Orchestrator Queue**.

- **Framework**: Basic Workflow Template
- **Main.xaml**: Entry point for extracting data and pushing to the queue
- **Typical Input**: Excel file, database, API
- **Output**: Queue items in Orchestrator (e.g., `TransactionQueue`)

### 2. ⚙️ Performer (`RPA_Performer`)
The **Performer** retrieves items from the Orchestrator queue and processes each transaction using business logic.

- **Framework**: Robotic Enterprise Framework (REFramework)
- **Main.xaml**: Entry point that orchestrates initialization, transaction handling, and closing
- **Input**: Orchestrator Queue Items
- **Output**: Processed data, logs, status updates, screenshots on error

---

## ⚙️ Configuration

Both Dispatcher and Performer use a configuration file named `Config.xlsx` (must be placed in the `Data` folder in the Performer project).

### Key Config Items:
- **OrchestratorQueueName**: Name of the queue (must match in both projects)
- **OrchestratorQueueFolder**: (Optional) Folder name if using modern folders
- **Application URLs or credentials** (Performer side)
- **Retry settings**, **Exception screenshots**, etc.

---

## 🧪 Testing

### Dispatcher
- Run the Dispatcher project
- Verify the queue items were added to the correct Orchestrator queue

### Performer
- Ensure the queue has items
- Run the Performer project
- Observe logging and transaction status in Orchestrator

---

## 🚀 Execution

### Order of Execution:
1. **Run Dispatcher** to load transactions into the queue
2. **Run Performer** to process each transaction item

### Execution Modes:
- Both projects support **Unattended** automation (Orchestrator execution)
- Can be run **Attended** in Studio or Assistant (for debugging)

---

## 🧩 Customization Guide

### To Add a New Process:
1. **Update `Process.xaml`** in the Performer with business rules
2. Adjust `GetTransactionData.xaml` if your queue items have a new schema
3. Ensure the Dispatcher matches the expected input format

### To Add New Applications:
- Modify `InitAllApplications.xaml` and `CloseAllApplications.xaml` in Performer

### To Add New Settings or Assets:
- Add to `Config.xlsx` or Orchestrator → Assets
- Retrieve using `Config("Key")` pattern

---

## 📁 Project Structure (Summary)

### Dispatcher
```
RPA_Dispatcher/
├── Main.xaml
├── project.json
└── (Other xamls or Excel files as needed)
```

### Performer
```
RPA_Performer/
├── Main.xaml
├── Framework/
│   ├── GetTransactionData.xaml
│   ├── InitAllSettings.xaml
│   ├── InitAllApplications.xaml
│   ├── Process.xaml
│   ├── SetTransactionStatus.xaml
│   └── CloseAllApplications.xaml
├── Data/
│   └── Config.xlsx
├── project.json
└── README.md
```

---

## 📌 Dependencies

Both projects rely on the following UiPath packages:
- `UiPath.System.Activities`
- `UiPath.UIAutomation.Activities`
- `UiPath.Excel.Activities`
- `UiPath.Testing.Activities` (Performer only)

> Ensure all dependencies are restored before publishing or running unattended.

---

## 🧠 Notes

- Exception handling and retry logic is built-in via REFramework
- System exceptions trigger screenshots (stored locally or uploaded)
- Logging is available through Orchestrator or local logs

---

## 📞 Support

For questions or issues, contact the automation developer or the RPA Center of Excellence (CoE).
