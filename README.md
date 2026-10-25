# MPI Customer Enquiry Automation

**AI-Assisted Lead Management | n8n | Google Gemini API | Google Sheets**

## 1. Project Overview

This project automates customer enquiry processing for Moti Packaging Industries (MPI), a packaging business. It uses n8n to orchestrate the workflow, Google Gemini to extract structured information from customer enquiries, and Google Sheets as a lightweight CRM and dashboard.

The workflow converts unstructured enquiry text into structured lead data, identifies missing information, flags enquiries for human review, and prepares customer follow-up drafts.

## 2. Objectives

- Automate customer enquiry processing.
- Extract product and order requirements from natural-language messages.
- Identify missing customer and delivery information.
- Check existing records for potential duplicate enquiries.
- Generate customer follow-up drafts.
- Store structured leads in Google Sheets.
- Track enquiry metrics through a dashboard.
- Keep customer communication subject to human approval.

## 3. Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow orchestration and automation |
| Google Gemini API | AI-powered enquiry extraction |
| Google Sheets | CRM storage and dashboard |
| JavaScript | Validation, data transformation and business rules |
| GitHub | Version control and project documentation |

## 4. Workflow Architecture

**Processing flow:**

Manual Trigger → Enquiry Input → Gemini Extract → Validate AI Response → Lookup Existing Enquiries → Check Duplicates and Draft Reply → Save Enquiry to Sheet

### Workflow Components

1. **Manual Trigger:** Starts a workflow execution.
2. **Enquiry Input:** Supplies the enquiry ID, source and raw enquiry text.
3. **Gemini Extract:** Sends the enquiry to the Gemini API and requests structured JSON.
4. **Validate AI Response:** Parses the AI response and normalizes fields for downstream processing.
5. **Lookup Existing Enquiries:** Retrieves existing CRM records.
6. **Check Duplicates and Draft Reply:** Checks for potential duplicates, identifies missing fields and prepares a follow-up draft.
7. **Save Enquiry to Sheet:** Appends the processed enquiry to the Google Sheets CRM.

## 5. Data Extracted

The workflow extracts or prepares the following fields:

- Customer name, company name and contact details
- Product category
- Diameter and height in millimetres
- Order quantity
- Product application
- Printing and artwork requirements
- Delivery location and required date
- Missing fields and conflicting fields
- Technical concerns
- Human-review requirement
- Lead status and follow-up draft

Unknown values are represented as missing or null values rather than being deliberately guessed.

## 6. Google Sheets CRM and Dashboard

The Google Sheets CRM stores the original enquiry alongside the extracted fields and workflow results.

The dashboard summarizes:

- Total enquiries
- Enquiries requiring additional information
- Enquiries requiring human review
- Enquiry errors

A chart provides a visual overview of enquiry metrics.

## 7. Human Review and Communication Safety

The workflow prepares follow-up messages as drafts. It does not automatically send these messages to customers.

Human review is required when information is missing, specifications need verification, or technical concerns require attention. Manufacturing capability, product suitability, pricing and delivery commitments must be confirmed by the appropriate team.

## 8. Testing and Results

An end-to-end test was performed using the test enquiry ID `MPI-TEST-004`.

**Sample enquiry:**

> We need 2000 paper cans, 80 mm diameter and 150 mm height for coffee packaging. Delivery to Delhi. Printed artwork required.

**Observed extraction results:**

| Field | Extracted value |
|---|---|
| Product category | Paper cans |
| Diameter | 80 mm |
| Height | 150 mm |
| Quantity | 2000 |
| Application | Coffee packaging |
| Printing requirement | Printed artwork required |
| Delivery location | Delhi |
| Lead status | More information required |
| Human review | Yes |

The workflow identified missing customer details and the required delivery date, generated a follow-up draft, and saved the processed record to Google Sheets.

## 9. Setup and Configuration

1. Import the exported workflow JSON into n8n.
2. Configure Google Sheets credentials and select the CRM spreadsheet and worksheet.
3. Configure the Gemini API key securely in the HTTP Request node or an appropriate credential configuration.
4. Verify the Gemini model endpoint and request body.
5. Confirm Google Sheets column mappings.
6. Run a test using a unique enquiry ID.
7. Verify the extracted values, lead status, follow-up draft and saved spreadsheet row.

## 10. Error Handling and Limitations

- Gemini API availability can vary; transient service errors may require retries.
- API errors and malformed responses should be handled and logged safely.
- Duplicate detection depends on the configured matching rules and available enquiry data.
- The workflow is a prototype and requires broader testing before production deployment.
- Technical specifications, manufacturing feasibility and quotations require human validation.
- Dashboard formulas depend on the spreadsheet's column layout.

## 11. Security

- Never commit API keys, access tokens or OAuth credentials to GitHub.
- Inspect exported workflow JSON before publishing it.
- Do not publish private customer enquiry data or unrestricted Google Sheets links.
- Use test data in screenshots and public documentation.
- Keep credentials in n8n's credential store or another secure secrets-management solution.

## 12. Future Improvements

- Add a dedicated error-handling and notification path.
- Implement a human approval step before customer communication.
- Improve duplicate detection using stable IDs and validated matching rules.
- Add more test cases for missing, conflicting and malformed information.
- Add lead-source and conversion metrics to the dashboard.
- Introduce production monitoring and controlled retries.

## 13. Project Status

**Prototype demonstrated:** Gemini-based extraction, response normalization, Google Sheets CRM integration, follow-up draft generation and dashboard metrics have been tested with sample enquiries.

**Next steps:** Expand failure-path testing, finalize approval handling, and validate the workflow under production-like conditions.

---

**Author:** Ayush Srivastava  
**Project:** MPI Customer Enquiry Automation  
**Purpose:** AI-assisted enquiry processing and lead management
