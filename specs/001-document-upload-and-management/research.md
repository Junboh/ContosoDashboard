# Research: Document Upload and Management

## Decision: Use local filesystem storage with SQLite metadata

**Rationale**:
- The ContosoDashboard training application must remain offline-capable and easy to run locally.
- SQLite is already used in the repository after the .NET 10 migration and is a lightweight database suitable for local training.
- Storing files outside `wwwroot` aligns with the existing security model and avoids exposing raw uploaded files directly.
- A local filesystem storage implementation keeps the feature simple while preserving a clean migration path to cloud storage later.

**Alternatives considered**:
- Use Azure Blob Storage: rejected because it adds external cloud dependency and breaks the offline training requirement.
- Keep SQL Server LocalDB: rejected because the project was already migrated to SQLite and the user requested SQLite.

## Decision: Use a local security validation stub for uploads

**Rationale**:
- The feature specification requires virus/malware scanning, but the app is training-focused and must not depend on an external AV service.
- A local validation stub can enforce the same high-level policies: allowed file types, file size limits, and safe filename handling.
- This allows the implementation to satisfy security intent while retaining offline compatibility.

**Alternatives considered**:
- Integrate a real antivirus engine: rejected because it is outside the training scope and adds platform-specific complexity.
- Defer scanning entirely: rejected because the feature explicitly requires upload validation and safe storage.

## Decision: Use a document metadata model with text tags and category values

**Rationale**:
- The specification explicitly calls for categories and tags, and a text-based model is simple for training.
- Storing category names as strings avoids the need for enum migrations or complex mapping.
- Tags can be stored as a normalized string list or simple comma-separated values to keep the first implementation small and maintainable.

**Alternatives considered**:
- Normalized tag table: rejected for initial implementation complexity.
- Numeric category IDs: rejected because the specification values are user-facing text categories.

## Decision: Add service-layer authorization for document access

**Rationale**:
- ContosoDashboard already enforces authorization at page and service layers.
- Document access must follow the same pattern for IDOR protection and training security.
- The existing role model (Employee, TeamLead, ProjectManager, Administrator) maps naturally to document ownership and project membership.

**Alternatives considered**:
- Page-only authorization: rejected because it leaves direct download endpoints vulnerable.
- No sharing model: rejected because the spec requires document sharing and notifications.
