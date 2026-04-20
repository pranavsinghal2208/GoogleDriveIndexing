# Labwerk Drive Index v2.1

An autonomous Google Drive indexing and auditing engine built for Architecture and Design firms. This tool converts a Google Drive environment into a structured database with automated security auditing and departmental categorization.

## 🚀 Overview

The **Labwerk Drive Index** solves the "where is that file?" problem by maintaining a real-time inventory of all files in Google Sheets. It is designed to handle thousands of files across Shared Drives and personal MyDrive spaces.

### Key Features
- **3-Phase Execution:** Full Indexing (Initial), Background Enrichment (Paths & Depts), and Delta Mode (Daily Sync).
- **AEC-Specific Logic:** Automatically identifies CAD, BIM, and Drawing files.
- **Security Audit:** Flags "High Risk" files based on public permissions and sensitive department classification.
- **Project Tracking:** Extracts project names directly from folder hierarchies.
- **Smart Summary:** Dashboard view for storage usage, file aging (Active/Stale/Archive), and duplicates.

---

## 🛠 Setup Instructions

### 1. Prerequisites
- A Google Workspace account.
- A new Google Sheet to serve as the Index.

### 2. Enable Services
In the Google Apps Script editor, you **must** enable the following Advanced Services:
1. **Drive API** (v3)
2. **Drive Activity API** (v2)

### 3. Installation
1. Open your Google Sheet.
2. Go to **Extensions** > **Apps Script**.
3. Paste the provided `Code.gs` into the editor.
4. Refresh your Google Sheet to see the **LABWERK Index** menu.

### 4. Initialization
1. Click the **LABWERK Index** menu and select **⚙ Setup (run first ever)**. This creates the required tabs and headers.
2. Select **▶ Run Full Index**.
   - *Note: The script will automatically create background triggers to finish the index if it takes longer than 6 minutes.*
3. Once completed, **Delta Mode** will auto-start to track daily changes at 7:00 AM.

---

## 📊 Columns Tracked
| Column | Description |
| :--- | :--- |
| `folder_path` | Full recursive path from Root to File. |
| `department` | Auto-classified (Finance, HR, Drawings, etc.). |
| `security_risk` | 🔴 High, 🟡 Medium, or 🟢 Low based on access. |
| `age_bucket` | Active, Stale (>6mo), or Archive (>2yr). |
| `is_duplicate` | Flags files with identical names. |

---

## ⚙ Configuration
You can modify the `CFG` object at the top of the script to change:
- **`triggerHour`**: When the daily Delta Sync runs (default 7 AM).
- **`maxDepth`**: How deep the folder path resolution should go (default 12).
- **Keywords**: Update the `classifyDepartment_` function to match your firm's specific folder naming conventions.

---

## 🛡 Disclaimer
*This tool is intended for internal auditing and management. Always review file permissions manually before taking action on "High Risk" items.*

**Author:** Built for LAB (Architecture Firm) via LABWERK.
