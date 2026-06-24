---
description: "Task list for Document Upload and Management feature"
---

# Tasks: Document Upload and Management

**Input**: Design documents from `/specs/001-document-upload-and-management/`
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, quickstart.md

## Phase 1: Setup (Shared Infrastructure)

- [ ] T001 Add `Document`, `DocumentShare`, and `DocumentActivity` model classes in `ContosoDashboard/Models/`
- [ ] T002 Add local storage configuration to `ContosoDashboard/appsettings.json` for document uploads
- [ ] T003 Create `IFileStorageService` and `LocalFileStorageService` in `ContosoDashboard/Services/`
- [ ] T004 Register `IFileStorageService` and `DocumentService` in `ContosoDashboard/Program.cs`
- [ ] T005 Add supported file type and size constants to `ContosoDashboard/Services/DocumentService.cs`
- [ ] T006 Add `DocumentUploadModel` and related view model classes in `ContosoDashboard/Models/`
- [ ] T007 Add new page routes for document upload, document listing, and document edit in `ContosoDashboard/Pages/_Imports.razor` or `ContosoDashboard/Program.cs`

---

## Phase 2: Foundational (Blocking Prerequisites)

- [ ] T008 Add `DbSet<Document>`, `DbSet<DocumentShare>`, and `DbSet<DocumentActivity>` to `ContosoDashboard/Data/ApplicationDbContext.cs`
- [ ] T009 Configure document entity relationships, indexes, and field lengths in `ContosoDashboard/Data/ApplicationDbContext.cs`
- [ ] T010 Implement local file path generation and secure storage location logic in `ContosoDashboard/Services/LocalFileStorageService.cs`
- [ ] T011 Implement a training-safe upload validation stub in `ContosoDashboard/Services/LocalFileStorageService.cs` that enforces allowed file types and 25 MB max size
- [ ] T012 Create `DocumentService` in `ContosoDashboard/Services/DocumentService.cs` to handle upload, search, preview, edit, delete, and share workflows
- [ ] T013 Add authorization checks for document ownership, project membership, and share access in `ContosoDashboard/Services/DocumentService.cs`
- [ ] T014 Add document activity logging support in `ContosoDashboard/Services/DocumentService.cs`
- [ ] T015 Add database initialization or migration notes for new document entities in `ContosoDashboard/README.md`

---

## Phase 3: User Story 1 - Upload and Organize Documents (Priority: P1)

**Goal**: Enable authenticated users to upload documents with required metadata, attach them to projects, and store files securely outside `wwwroot`.

**Independent Test**: Upload a supported document with title, category, and optional project assignment, then confirm the document appears in the user’s document list.

- [ ] T016 [US1] Create `Pages/DocumentUpload.razor` for file selection, metadata entry, category selection, project association, and progress feedback
- [ ] T017 [US1] Implement upload form validation in `Pages/DocumentUpload.razor` and `ContosoDashboard/Services/DocumentService.cs`
- [ ] T018 [US1] Implement secure file save and metadata persistence in `ContosoDashboard/Services/DocumentService.cs`
- [ ] T019 [US1] Implement local filesystem storage and unique path generation in `ContosoDashboard/Services/LocalFileStorageService.cs`
- [ ] T020 [US1] Add success and error handling UI feedback for document upload in `Pages/DocumentUpload.razor`
- [ ] T021 [US1] Add upload metadata persistence and project association in `ContosoDashboard/Data/ApplicationDbContext.cs`

---

## Phase 4: User Story 2 - Browse, Search, and Preview Documents (Priority: P2)

**Goal**: Enable users to find accessible documents quickly, preview browser-friendly files, and download authorized documents.

**Independent Test**: Search by title or tag, verify result filtering by authorization, and preview a PDF or image document.

- [ ] T022 [US2] Create `Pages/Documents.razor` for document listing, search, filtering, sorting, and preview/download actions
- [ ] T023 [US2] Implement search and filter logic in `ContosoDashboard/Services/DocumentService.cs`
- [ ] T024 [US2] Add document preview support for PDF and image files in `Pages/Documents.razor`
- [ ] T025 [US2] Add authorized download handling in `ContosoDashboard/Services/DocumentService.cs`
- [ ] T026 [US2] Add project document list support to `Pages/ProjectDetails.razor`
- [ ] T027 [US2] Add document access filtering so users see only documents they uploaded, documents shared with them, or project documents they are authorized to view

---

## Phase 5: User Story 3 - Manage Document Metadata and Sharing (Priority: P3)

**Goal**: Allow document owners to edit metadata, replace files, delete documents, and share documents with other users or teams.

**Independent Test**: Update metadata for a document, replace the file, and confirm the changes are reflected in the document list.

- [ ] T028 [US3] Create `Pages/DocumentEdit.razor` for editing title, description, category, tags, and replacing the file
- [ ] T029 [US3] Implement document metadata update workflow in `ContosoDashboard/Services/DocumentService.cs`
- [ ] T030 [US3] Implement file replacement workflow in `ContosoDashboard/Services/DocumentService.cs`
- [ ] T031 [US3] Add delete confirmation and removal logic in `Pages/Documents.razor` and `ContosoDashboard/Services/DocumentService.cs`
- [ ] T032 [US3] Implement document sharing support and shared-document notification generation in `ContosoDashboard/Services/DocumentService.cs` and `ContosoDashboard/Services/NotificationService.cs`
- [ ] T033 [US3] Add a shared documents view and notification handling in `Pages/Documents.razor`

---

## Phase 6: Polish & Cross-Cutting Concerns

- [ ] T034 [P] Add authorization attributes and service-level access checks to all document pages and service methods
- [ ] T035 [P] Add or update relevant documentation in `README.md` and `specs/001-document-upload-and-management/quickstart.md`
- [ ] T036 [P] Refine input validation, error messages, and upload progress UX in `Pages/DocumentUpload.razor`
- [ ] T037 [P] Add todos or comments for any unresolved edge cases in documentation files
- [ ] T038 [P] Verify local file storage path and cleanup rules in `ContosoDashboard/appsettings.json` and `ContosoDashboard/Services/LocalFileStorageService.cs`

---

## Dependencies & Execution Order

- Phase 1 tasks establish shared storage and page wiring.
- Phase 2 tasks implement the document data model, secure file storage, and service layer infrastructure.
- User Story phases depend on foundational services and the document model being in place.
- User Story tasks are designed to be independently testable after Phase 2 completes.

## Parallel Opportunities

- Phase 1 tasks `T002`, `T003`, and `T004` can run in parallel because they configure service registration and infrastructure separately.
- Phase 2 tasks `T010`, `T011`, and `T014` can run in parallel because they implement separate service and validation concerns.
- Phase 6 polish tasks `T034` through `T038` can run in parallel as cross-cutting cleanup and documentation work.

## Implementation Strategy

1. Complete setup and foundational tasks to add the document model, storage abstraction, and service layer.
2. Deliver User Story 1 first so upload and secure storage are functional end-to-end.
3. Add search, preview, and authorized browsing in User Story 2.
4. Add metadata editing, replacement, delete, and sharing support in User Story 3.
5. Finalize with authorization checks, UX refinements, and documentation updates.
