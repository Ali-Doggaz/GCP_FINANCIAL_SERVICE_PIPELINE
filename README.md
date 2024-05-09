# GCP FINANCIAL SERVICE PIPELINE PROJECT

![archi_diagram-tp4 (3)](https://github.com/Ali-Doggaz/GCP_FINANCIAL_SERVICE_PIPELINE/assets/62618334/e361c8ed-35f0-4281-8f4d-f8c551223abb)

## Data Sources
- **Google Form with File Upload**: Collects initial data and documents from users, which are then uploaded and stored in Cloud Storage.

## Data Ingestion
- **Pub/Sub Topic**: Acts as a messaging hub, receiving notifications from Google Forms about new data submissions.
- **Cloud Storage**: Stores uploaded files and data from Google Forms, serving as the initial repository before processing.

## Processing
### Commercial Service
- **Cloud Function**: Triggered by Pub/Sub, performs initial Extract, Transform, Load (ETL) operations on incoming data.
- **Private Bank DB (Cloud SQL)**: Processes transactions and stores results in a relational database, interfacing with the commercial service logic.

### Risk Management Service
- **Vision AI (OCR)**: Optical Character Recognition processes documents to extract text and relevant data.
- **Pub/Sub Topic**: Further communicates the processed data for subsequent risk analysis.
- **Cloud Function (ETL/Enrich)**: Additional ETL tasks to enrich and prepare data for decision-making processes.

### Credit Agreement Service
- **Cloud Run**: Makes final credit decisions based on enriched data, outputs agreements or disapprovals.
- **Cloud Storage**: Stores final documents relating to credit agreements securely.

## Integration with External Services
- **Central Bank API Endpoint**: Connects to external central bank services for compliance checks and additional data validation.
- **Gmail API**: Sends notification emails to users about the status of their credit applications, using the processed and stored data.

