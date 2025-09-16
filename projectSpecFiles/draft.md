I have a project in mind, It's going to be a git-based document control for the flying school I work at. Although this should work for any company that has the problem of documents not being controlled well.

# The problem

The current problem we sit with at work is that we have a lot of documents floating around, various versions of each and a there are a lot of changes that don't get synced up properly, so often there is outdated information about certain flying concepts or something that is not properly explained.

# My solution

My goal would be to have a document that can do the following.

1. Have one central source of truth.
2. There should only be one source of truth for anything. So if there is a description for the procedures in how to fly a base turn stall, then this should only be mirrored in other sections, not redefined.
3. Be easily editable by various persons, instructors and students, but the edits should only be apporaved by a management layer.
4. be searchable in a complex way of building up sections just by searching.

- If I need to know everything about take offs, it will get all elements tagged with take off, this will include procedures, policies, limitations, restrictions etc. Then I should be able to filter more to only show limitations or only procedures.

# Permissions

- Users should be split between the following roles:
  - Viewer
  - Editor
  - Manager
    (These role labels can be changed depending of the use cases)
- Viewers can only view the docs
- Editors can change the documentation - but these are just suggested changes and must be approaved by managers
- Instant edits can be done and changes made by other users can be approved

# Notifications

- Managers should get notifications if there are edits that need to be reviewed and approved
- Editors will get a notification if there edit was merged or rejected and if rejected a reason why
- All users will get a stream on notifications based only on merges if the merge has been successfully megred

# Document structure

- The document will be structured in a hierarchical structure similar to atomic design principals

## The parts of the structure

- The following will be ELEMENTS
- Heading
- Subheading
- Sentence
- Image
- Image caption
- List
- List item

- The following will be COMPONENTS

  - A paragraph (Collection of sentences)
  - List section (List and list items)
  - Heading section (Heading and sub heading)
  - Image section (An image and it's caption)

- The following will be SECTIONS
  - A section will be a number of components put together
  - A heading section with some paragraphs and some lists and some images but all related to one topic
