# Clarifying Questions for Git-Based Document Control Tool

## Core Functionality
1. **User Interface**: Do you envision this as a web application, desktop app, or CLI tool?

2. **Document Organization**: How should documents be organized? Folder-based hierarchy, flat structure with tags only, or both?

3. **Tagging System**:
   - What types of elements should be taggable? (paragraphs, images, videos, entire documents?)
   - Should tags be hierarchical (like categories/subcategories) or flat?
   - Any specific tag formats or naming conventions?

## Media Handling
4. **Media Storage**: Should images and videos be stored in the git repo directly, or referenced from external storage (cloud, CDN)?

5. **Media Types**: What specific formats should be supported? (PNG, JPG, MP4, WebM, etc.)

6. **Media Processing**: Do you need automatic thumbnail generation, compression, or format conversion?

## Git Integration
7. **Version Control**: Should users interact with git directly, or should it be abstracted behind a user-friendly interface?

8. **Collaboration**: How should multiple users collaborate? Branch-based workflows, direct commits, or merge request approvals?

9. **Conflict Resolution**: How should conflicts in document edits be handled?

## Technical Architecture
10. **Technology Stack**: Any preferences for frontend/backend technologies?

11. **Deployment**: Self-hosted, cloud-based, or both options?

12. **Authentication**: User management requirements? (single user, teams, organizations?)

## Document Features
13. **Search**: Should there be full-text search across documents and tags?

14. **Export**: Need to export to other formats (PDF, HTML, etc.)?

15. **Templates**: Should there be document templates or structured document types?