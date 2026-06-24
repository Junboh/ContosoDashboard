# Quickstart: Document Upload and Management

## Prerequisites

- .NET 10 SDK installed
- Local SQLite support available through the .NET runtime
- Project dependencies restored (`dotnet restore`)
- Application configured to use SQLite and local file storage

## Setup

1. Open the repository root:

   ```bash
   cd /Users/fujiwarajunya/work/VSCode/test/TrainingProjects/ContosoDashboard/ContosoDashboard
   ```

2. Restore packages:

   ```bash
   dotnet restore
   ```

3. Build the project:

   ```bash
   dotnet build
   ```

4. Run the application:

   ```bash
   dotnet run
   ```

5. Open the browser at `http://localhost:5000`.

## Validation Scenarios

### Scenario 1: Upload a supported document

1. Login as a training user.
2. Navigate to the document upload page.
3. Select a supported file (PDF, Word, Excel, PowerPoint, text, JPEG, or PNG).
4. Enter a title, select a category, and optionally associate a project.
5. Upload the file.
6. Expected: upload succeeds, metadata is saved, and file appears in your document list.

### Scenario 2: Reject unsupported file type or oversized file

1. Upload a file larger than 25 MB or with an unsupported extension.
2. Expected: the application rejects the file and displays a clear error message.

### Scenario 3: Search and preview a document

1. Navigate to the document search page.
2. Search by title, tag, uploader, or project.
3. Expected: matching documents appear, filtered by your access rights.
4. Preview a PDF or image file.
5. Expected: the document displays in the browser.

### Scenario 4: Edit document metadata and replace a file

1. Open a document you uploaded.
2. Update the title, category, or tags.
3. Upload a new version of the file.
4. Expected: metadata updates and the new file is stored.

### Scenario 5: Delete a document

1. Delete a document you own.
2. Expected: the document is removed from the list and the file is deleted from storage after confirmation.

## Notes

- The initial implementation stores documents in the local filesystem outside `wwwroot`.
- Metadata is persisted in SQLite.
- If the app is restarted, the SQLite database and local files should remain available.
- Verify the upload directory path in `appsettings.json` or configuration if the filesystem storage location changes.
