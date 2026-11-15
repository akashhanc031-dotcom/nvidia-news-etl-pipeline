# NVIDIA AI & Data Center News Monitor (ETL Pipeline)

## 📖 Project Overview
This is an independent data engineering portfolio project built using **n8n**. It is a fully automated ETL (Extract, Transform, Load) pipeline that monitors public NVIDIA news releases, filters for relevant AI and computing topics, standardizes the data schema, and automatically emails a CSV report to the user every morning at 8:00 AM.

*Disclaimer: This is an independent learning exercise and is not affiliated with NVIDIA.*

## ⚙️ Architecture
![Workflow Canvas](images/workflow-canvas.jpeg)

### The ETL Process:
1. **Trigger:** Schedule Trigger (runs daily at 8:00 AM).
2. **Extract:** RSS Read node (pulls from `nvidianews.nvidia.com`).
3. **Filter:** IF/Filter node using Regex (`AI|GPU|Blackwell|data center|computing`) to reduce data noise by 50%.
4. **Transform:** Edit Fields node (maps raw XML to a clean 4-column schema: Title, Published Date, Article URL, Description).
5. **Load:** Convert to File node (generates a CSV).
6. **Deliver:** Send Email (SMTP) node (securely emails the CSV attachment using a Google App Password).

## 📊 Results
### Cleaned Data Output
![Cleaned Data](images/cleaned-data.jpeg)

### Automated Email Delivery
![Email Delivery](images/email-delivery.jpeg)

## 📝 Key Learnings & Limitations
* **Schema Mapping:** Learned how to strip away unstructured, messy JSON and enforce a strict schema for downstream consumption.
* **Security:** Configured secure SMTP delivery using Google App Passwords rather than exposing primary account credentials.
* **Limitations:** This pipeline does not feature persistent deduplication. If NVIDIA releases the same article twice, it will be sent twice. A future improvement would be to add a database lookup step (e.g., PostgreSQL or Redis) to track historical GUIDs.
