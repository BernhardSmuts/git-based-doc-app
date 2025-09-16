# Git-Based Document Control System - Project Specifications

**Single Source of Truth for Project Requirements**

## Project Overview

A web-based document control system using git for version control, designed for organizations needing controlled collaborative document editing with approval workflows. Initially designed for flying schools but built to be industry-agnostic.

## Core Problem Statement

Organizations struggle with document version control where:
- Multiple versions of documents exist without clear authority
- Changes don't sync properly across teams
- Outdated information persists in circulation
- No centralized approval process for critical information

## Solution Architecture

### Document Structure (Atomic Design Approach)

**Hierarchy**: Documents ’ Sections ’ Components ’ Elements

#### Elements (Atomic Level)
- Heading
- Subheading
- Sentence
- Image
- Image caption
- List
- List item
- Checklist item (challenge-response format: "FLAPS ... LAND")

#### Components (Molecular Level)
- Paragraph (collection of sentences)
- List section (list + list items)
- Heading section (heading + subheading)
- Image section (image + caption)

#### Sections (Organism Level)
- Collection of components around one topic
- Combination of heading sections, paragraphs, lists, images

#### Documents (Page Level)
- Collection of sections forming complete documents

### Unique Identification System

- **Every element has a UUID**
- **Every component has a UUID**
- **Every section has a UUID**
- **Every document has a UUID**
- **Structure defined by JSON tree of nested UUIDs**

### Content Relationship System

- JSON reference table defines parent/peer/child relationships
- Elements can be reused across multiple components/sections
- Single source of truth: content defined once, referenced everywhere
- No content duplication - only UUID references

## User Roles & Permissions

### Viewer
- Read-only access to approved documents
- Cannot edit or suggest changes

### Editor
- Can activate edit mode on any document
- Create/modify/delete content using WYSIWYG interface
- Submit changes as pull requests to managers
- View personal edit history (pending/approved/rejected)
- Access rejection reasons for declined edits

### Manager
- All editor permissions
- Approve/reject pending edits with granular control
- Can approve individual elements or bulk approve sections
- Must provide rejection reasons
- Receive notifications for pending approvals

## Technical Implementation

### Version Control (Git Integration)
- Each edit creates a separate branch from master
- Branch naming: username of editor
- Master branch = approved/live content
- Pull request workflow for edit approval
- Complete audit trail of all changes

### Content Management
- Document version controlled by total document checksum
- Incremental sync using checksum diff validation
- Offline capability via service workers
- Clear version mismatch indicators with sync options

### Search & Tagging System
- Manual tag assignment by content creators
- Tags enable complex content aggregation
- Example: Search "takeoffs" returns all tagged elements (procedures, policies, limitations)
- Filter results by content type or tag specificity

## User Experience Design

### Editing Workflow
1. User activates edit mode on document
2. WYSIWYG editor appears with MS Word-style toolbar (markdown-compatible features only)
3. User makes changes (add/edit/remove text, images, etc.)
4. User clicks submit ’ creates pull request
5. Managers receive notification for review

### Approval Interface
- GitHub-style diff view (red minus, green plus)
- Individual checkboxes for granular approval
- "Select all" option for bulk approval
- Mandatory rejection reason field
- Clear approve/reject action buttons

### Editor Dashboard
- View pending edits with diff preview
- Edit history (approved/rejected with reasons)
- Status indicators for all submissions

### Notification System
- Real-time in-app notifications only
- Managers: notified of pending approvals
- Editors: notified of approval/rejection decisions
- All users: notified of successful merges

## Content Features

### Text Formatting
- Basic markdown-equivalent formatting
- Text color and background color options
- Standard rich text features (bold, italic, lists, etc.)

### Content Types
- Standard text and images
- Checklist items with challenge-response format
- Lists and numbered lists
- Headings with hierarchy

### Content Referencing
- UUID-based content reuse
- Single definition, multiple references
- Automatic updates across all references when source content changes

## Offline & Sync Capabilities

### Offline Access
- Service worker implementation for offline functionality
- Ability to cache specific sections for offline study
- Clear offline/online status indicators

### Version Synchronization
- Checksum-based version validation
- Incremental diff sync from last valid checksum
- Conflict resolution for concurrent edits
- Automatic sync on connection restoration

## Future Considerations

### Scalability
- Single organization deployment initially
- No inter-company document sharing
- Self-contained document ecosystem per deployment

### Performance
- Checksum-based incremental loading
- Efficient diff-based synchronization
- Optimized for collaborative editing workflows

## Technical Stack Requirements

- Web-based application (no mobile app initially)
- Git backend for version control
- Real-time notification system
- WYSIWYG editor component
- UUID generation and management
- JSON-based structure storage
- Checksum generation for version control
- Service worker for offline capability

## Success Metrics

1. Single source of truth maintained (no content duplication)
2. All edits properly tracked and attributed
3. Clear approval workflow with audit trail
4. Efficient content discovery through tagging
5. Reliable offline access for study purposes
6. Fast sync and conflict resolution

---

*This specification serves as the definitive requirements document for the git-based document control system project.*