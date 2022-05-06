# TuitionCo Design Document 1-Pager

### Feature Requirements Overview

1. Can handle CSVs in multiple, pre-defined formats
2. Provides a management portal to approve or deny users
3. Provides a management portal to release invoices to customer
4. Generate invoice in CSV format
5. Provide a secure API for 3rd-party integrations

### Goals

- Support a highly scalable model
- Create single API points, regardless of web, cli or service
- Decoupled processing

### Assumptions

- Security concerns, such as defining the authN/authZ models, are out of scope
- A secured and valid API gateway is in place
- CI/CD is out of scope, but would recommend infrastructure as code
- Partners don't require feedback on the CSV processing status
- The "standard" AWS technologies will be used unless otherwise noted (checkout dapr.io sometime, it's super sexy)

## Architecture Overview

<DIAGRAM>

The new system uses secured APIs for all internal actions, both external 3rd-parties uploading data and the internal invoice management portal.

All backend processing of CSVs and invoices are handled in producer/consumer fashion, with the producer using message queues to inform the processing consumers.

### System Components

#### 1 - Client Apps

Client Apps represent any user of the system wishing in push a CSV to TuitionCo for processing. This can be either direct API usage or by uploading the CSV to either an FTP or S3 location, both of which will trigger a lambda that will inturn call the Ingestion API for processing.

#### 2 - Ingestion API

The Ingestion API is a light-weight microservice responsible for ingesting CSV expense files for processing. It can handle either the CSV data directly as part of the POST payload or a URL to an accessible URL for processing.

```
# Upload CSV
# the optional {csv-route} portion of the route determines which
# CSV processor to use, defaults to TuitionCo's publicly defined
# standard
#
# 202 on success since processing is handled async
POST /api/ingest/{csv-format}

{
    "csv_url": "http://whiskeyanecode.com/2022-01-25.expenses.csv"
    "expenses": [
        {   }
    ]
}
```

- `csv-format` is one of N predefined supported CSV formats
- custom formats could be added at a later date if business needs require it
- defining the format of `expenses` is out of scope for this document

Regardless of the method used the CSV file will be copied to a secure location inside the platform for later processing and then a message will be queued in the `CSV Message Queue`

#### 3 - CSV Storage

This is Amazon S3 (or whatever works best, I've been deep in the Azure stack for two years so would need a refresher).

#### 4 - CSV Message Queue

Messages are queued with a CSV file URL and CSV file format. These messages are picked up and processed by the CSV Message Processor.

#### 5 - CSV Message Processor

The CSV Message Processor is responsible for removing an item out of the CSV Message Queue and processing it, using the correct CSV parser. Given the possible large nature of the files it's important to separate out the processing of the files from any UI actions.

- Special consideration should be payed to errors at this stage. Not pictured is an error queue where failed CSV parser attempts are sent for debugging or re-trying.
- In a later design stage a job ID should be attached to each incoming CSV parser request that the partner can use to check the status of their uploaded CSV files
- A retention policy for both successful and failed incoming CSV files needs to be discussed

As the CSV file is parsed each individual expense is added as a message to the Expense Message Queue, in real-time as it's parsed instead of waiting for the entire file to be processed.

#### 6 - Expense Message Queue

Messages contain user, expense, company. These message are picked up by the Expense Processing Queue

#### 7 - Expense Processing Queue

The Expense Processing Queue handles taking items out of the Expense Message Queue and adding them to the system via the Billing API. Business rule validation can be applied here for each line item, based on business need.

- Note: instead of calling the API directly the internal service-to-service communication method should be used, if there is one. This can be pub/sub or another message queue, but internal service using HTTP is an anti-pattern. This should be consistent for all services within a platform and is an important point of consistency.

#### 8 - Billing API

The Billing API could easily be split into two services, one for managing expenses, the other for creating invoices, but the diagram explodes a bit at that point.

```
# add one or more expenses
# used by the Expense Processing Queue
POST /api/expense

[
  {
    "user": "Shawn Oster",
    "expense": "2.00",
    "company": "Mighty AI",
    "type": "tuition"
  },
  {
    "user": "Kurt Cobain",
    "expense": "87.00",
    "company": "Nirvana",
    "type": "tuition"
  }
]
```

Invoice management is also handled via this API with the following APIs:

```
GET /api/invoice?pageSize=100&pageNum=1  # returns a paginated list of invoices, can also be filtered by user, date, status
GET /api/invoice/{invoiceId}             # return a specific invoice
```

#### 9 - Billing DB

This is where each expense is stored, in a relational database. More information is needed on how these expenses are used in other parts of the company.

The database is ONLY accessible via the Billing API, and should be secured in such a way that only admins and SREs have direct access, and strictly for debugging or forensic reasons. This also contains PII and most likely is also subject to GDPR take downs.

#### 10 - Invoice Management UI

This UI only depends on the Billing API and thus should require little to to no involvement from other teams in order to generate a UI to review and release invoices. All operations that the UI performs will be handled by the Billing API.