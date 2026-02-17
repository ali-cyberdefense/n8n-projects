**The Problem:** Manual extraction of data from Monthly Business Reports (MBR) is error-prone and consumes hours of operations time.

**The Solution:** An end-to-end ETL (Extract, Transform, Load) pipeline that triggers upon file upload, processes raw data, and updates a centralized executive dashboard.

**Technical Highlights:**

Dynamic File Handling: Uses Google Drive triggers to detect new uploads and extract data without manual naming conventions.

Data Transformation: Leverages n8n expressions and the Code Node to parse dates, normalize strings, and perform mathematical summations across specific columns.

State Management: Automatically identifies the reporting month from metadata to ensure data is appended to the correct row in the master Google Sheet.
