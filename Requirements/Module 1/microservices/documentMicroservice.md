# Document Generation Microservice

## Overview

The **Document Generation Microservice** handles:

- **Generating digital and physical documents** based on templates.
- **Converting HTML content** into formats like PDF or DOCX.
- **Storing generated documents** in Azure Blob Storage.
- **Providing endpoints** to retrieve and download stored documents.
- **Uploading and managing scanned documents**.
- **Emitting events** such as `DocumentGenerated`, `DocumentStored`, and `DocumentUploaded`.

---

## Entities

### Document

Represents a generated or uploaded document.

- **id**: Unique identifier of the document.
- **userId**: ID of the user associated with the document.
- **fileName**: Name of the document file.
- **fileType**: MIME type (e.g., `application/pdf`, `image/jpeg`).
- **storageUri**: URI where the document is stored in Azure Blob Storage.
- **documentType**: Indicates if the document is generated or uploaded (`generated`, `uploaded`).
- **metadata**: Additional information (e.g., template ID for generated documents).
- **createdAt**: Timestamp when the document was created or uploaded.

---

## API Endpoints

### 1. Generate Document

- **Endpoint**: `POST /documents/generate`
- **Description**: Generates a document from a template.

**Request Parameters**:

- **templateId**: ID of the template to use.
- **contextId**: Identifier for fetching rendered template data.
- **outputFormat**: Desired format (`pdf`, `docx`, `html`).
- **isPhysical** (optional): Whether a physical copy is needed.

**Example Request**:

```http
POST /documents/generate
Content-Type: application/json
Authorization: Bearer <token>

{
  "templateId": "template-123",
  "contextId": "user-456",
  "outputFormat": "pdf",
  "isPhysical": false
}
```

**Example Response**:

```json
{
  "documentId": "doc-789",
  "storageUri": "https://blobstorage.com/documents/doc-789.pdf",
  "fileName": "Generated_Document.pdf",
  "fileType": "application/pdf",
  "documentType": "generated",
  "isPhysical": false,
  "createdAt": "2023-10-01T12:00:00Z"
}
```

---

### 2. Upload Scanned Document

- **Endpoint**: `POST /documents/upload`
- **Description**: Uploads a scanned document to the system.

**Request Parameters**:

- **file**: The scanned document file to upload.
- **metadata** (optional): Additional information about the document (e.g., document category, tags).

**Example Request**:

```http
POST /documents/upload
Authorization: Bearer <token>
Content-Type: multipart/form-data

{
  "file": <scanned_document.pdf>,
  "metadata": {
    "category": "Identity Proof",
    "tags": ["passport", "verification"]
  }
}
```

**Example Response**:

```json
{
  "documentId": "doc-1011",
  "storageUri": "https://blobstorage.com/documents/doc-1011.pdf",
  "fileName": "Passport_Scan.pdf",
  "fileType": "application/pdf",
  "documentType": "uploaded",
  "createdAt": "2023-10-01T13:00:00Z"
}
```

---

### 3. Retrieve Document Metadata

- **Endpoint**: `GET /documents/{id}`
- **Description**: Retrieves metadata for a specific document.

**Example Request**:

```http
GET /documents/doc-1011
Authorization: Bearer <token>
```

**Example Response**:

```json
{
  "documentId": "doc-1011",
  "userId": "user-456",
  "fileName": "Passport_Scan.pdf",
  "fileType": "application/pdf",
  "storageUri": "https://blobstorage.com/documents/doc-1011.pdf",
  "documentType": "uploaded",
  "metadata": {
    "category": "Identity Proof",
    "tags": ["passport", "verification"]
  },
  "createdAt": "2023-10-01T13:00:00Z"
}
```

---

### 4. Download Document

- **Endpoint**: `GET /documents/{id}/download`
- **Description**: Downloads the stored document.

**Example Request**:

```http
GET /documents/doc-1011/download
Authorization: Bearer <token>
```

**Response**:

- Returns the document file for download.

---

## Scan Upload Use Case

### Purpose

Allows users to upload scanned documents (e.g., identity proofs, signed contracts) to be stored and managed within the system.

### Workflow

1. **User Uploads a Scanned Document**:

   - The user sends a `POST` request to `/documents/upload` with the scanned document file and optional metadata.

2. **Document Storage**:

   - The service stores the uploaded file in Azure Blob Storage.
   - Generates a unique `documentId` for the document.
   - Records metadata and associates it with the user.

3. **Emit Event**:

   - The service emits a `DocumentUploaded` event containing details about the uploaded document.

4. **Response to User**:

   - Returns a response containing the `documentId`, storage URI, and other relevant details.

### Example Scenario

- **Use Case**: A user needs to submit a scanned copy of their passport for verification.

- **Steps**:

  1. The user accesses the application interface to upload their passport scan.
  2. They select the scanned PDF file and submit it via the upload endpoint.
  3. The Document Generation Microservice stores the file and returns the document details.
  4. The system can now use this document for verification processes.

---

## Domain Events

### DocumentUploaded

- **Emitted When**: A scanned document is successfully uploaded and stored.

- **Contains**:

  - `documentId`
  - `userId`
  - `fileName`
  - `fileType`
  - `storageUri`
  - `metadata` (e.g., category, tags)
  - `timestamp`

**Example Event Payload**:

```json
{
  "eventType": "DocumentUploaded",
  "documentId": "doc-1011",
  "userId": "user-456",
  "fileName": "Passport_Scan.pdf",
  "fileType": "application/pdf",
  "storageUri": "https://blobstorage.com/documents/doc-1011.pdf",
  "metadata": {
    "category": "Identity Proof",
    "tags": ["passport", "verification"]
  },
  "timestamp": "2023-10-01T13:00:00Z"
}
```

---

## Key Points

- **Scan Upload Capability**: Users can upload scanned documents, which are stored and managed alongside generated documents.

- **Unified Document Management**: Both generated and uploaded documents are treated similarly, allowing for consistent retrieval and management.

- **Endpoints Provided**: The `/documents/upload` endpoint allows for uploading, while existing endpoints support retrieval and download.

- **Event Emission**: The `DocumentUploaded` event allows other services to react to new uploads (e.g., triggering verification workflows).

- **Security Considerations**:

  - **File Validation**: Uploaded files are validated to ensure they are of acceptable types and sizes.
  - **Access Control**: Only authorized users can upload and access documents.

---

## Additional Notes

- **Metadata Usage**: Metadata provided during upload can be used to categorize and search for documents.

- **Supported File Types**: The service may restrict uploads to certain file types (e.g., PDF, JPEG, PNG).

- **Storage**: Uploaded documents are stored securely in Azure Blob Storage, similar to generated documents.

- **Error Handling**:

  - **Invalid File Type**: Returns a `400 Bad Request` if the file type is not supported.
  - **File Too Large**: Returns a `413 Payload Too Large` if the file exceeds size limits.
  - **Authentication Errors**: Returns `401 Unauthorized` if the user is not authenticated.

---

## Examples

### Uploading a Scanned Document

**Request**:

```http
POST /documents/upload
Authorization: Bearer <token>
Content-Type: multipart/form-data

{
  "file": <passport_scan.pdf>,
  "metadata": {
    "category": "Identity Proof",
    "tags": ["passport", "verification"]
  }
}
```

**Service Actions**:

- Validates the file type and size.
- Stores the file in Azure Blob Storage.
- Saves metadata and associates the document with the user.
- Emits a `DocumentUploaded` event.

**Response**:

```json
{
  "documentId": "doc-1011",
  "storageUri": "https://blobstorage.com/documents/doc-1011.pdf",
  "fileName": "Passport_Scan.pdf",
  "fileType": "application/pdf",
  "documentType": "uploaded",
  "createdAt": "2023-10-01T13:00:00Z"
}
```

---

### Retrieving an Uploaded Document's Metadata

**Request**:

```http
GET /documents/doc-1011
Authorization: Bearer <token>
```

**Response**:

```json
{
  "documentId": "doc-1011",
  "userId": "user-456",
  "fileName": "Passport_Scan.pdf",
  "fileType": "application/pdf",
  "storageUri": "https://blobstorage.com/documents/doc-1011.pdf",
  "documentType": "uploaded",
  "metadata": {
    "category": "Identity Proof",
    "tags": ["passport", "verification"]
  },
  "createdAt": "2023-10-01T13:00:00Z"
}
```

---

## Integration with Other Services

- **Verification Processes**: Uploaded documents can be used by other services for identity verification or compliance checks.

- **Notifications**: The `DocumentUploaded` event can trigger notifications or workflows in other systems.

---