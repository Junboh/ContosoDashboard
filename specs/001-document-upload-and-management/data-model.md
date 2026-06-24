# Data Model: Document Upload and Management

## Entities

### Document
- **DocumentId**: integer, primary key
- **Title**: string, required
- **Description**: string, optional
- **Category**: string, required
- **Tags**: string, optional (stored as comma-separated values or JSON text)
- **FilePath**: string, required, stores the local filesystem path or relative storage key
- **FileName**: string, required, original filename for display
- **ContentType**: string, required, MIME type
- **FileSize**: long, required, size in bytes
- **UploadDate**: DateTime, required
- **UploadedByUserId**: integer, required, foreign key to `User`
- **ProjectId**: integer, optional, foreign key to `Project`
- **IsShared**: bool, required, derived field to indicate shared documents
- **IsDeleted**: bool, required, soft-delete flag if implemented later

### DocumentShare
- **DocumentShareId**: integer, primary key
- **DocumentId**: integer, required, foreign key to `Document`
- **SharedWithUserId**: integer, required, foreign key to `User`
- **SharedByUserId**: integer, required, foreign key to `User`
- **SharedDate**: DateTime, required
- **AccessLevel**: string, optional, e.g. "Read"

### DocumentActivity
- **DocumentActivityId**: integer, primary key
- **DocumentId**: integer, required, foreign key to `Document`
- **UserId**: integer, required, foreign key to `User`
- **ActivityType**: string, required, values such as "Upload", "Download", "Delete", "Share"
- **ActivityDate**: DateTime, required
- **Details**: string, optional

## Relationships
- `User` 1→* `Document` via `UploadedByUserId`
- `Project` 1→* `Document` via `ProjectId`
- `Document` 1→* `DocumentShare` via `DocumentId`
- `Document` 1→* `DocumentActivity` via `DocumentId`

## Notes
- Document file metadata is separate from the file contents, which are stored on the local filesystem outside of `wwwroot`.
- Categories are stored as text to preserve training simplicity and avoid enum migration overhead.
- Tags can be implemented as a simple string list in the first iteration; the model can evolve later if needed.
