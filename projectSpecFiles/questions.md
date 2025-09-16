# Questions & Clarifications for Git-Based Document Control System

Based on your draft.md concepts, here are some questions to help clarify and refine the project specifications:

Note: This will be a web-based app

## Technical Architecture Questions

1. **Git Integration**: How should the git-based versioning work? Should each document change create a git commit, or should we batch changes? Should we use branches for pending edits awaiting approval?

- Each change can effectively be a sererate branch from the master branch at that time. The branch name can be the username of the person that created it.

2. **Search & Tagging**: For your complex search functionality (e.g., "everything about takeoffs"), how should the tagging system work? Should tags be:
   - Manually assigned by editors? (Yes)
   - Auto-generated from content analysis? (No)
   - A combination of both? (No)
   - Hierarchical (e.g., `procedures.takeoff.crosswind`)? (No)

- This will be assigned by the person creating the content. Initially this will be a lot of work, but once it's done it will allow for complex structres to be built purely procedural.
- Each element will have a unique ID and there will be a structure tree basically used to build the structure and the hierarchy (This can be a JSON based structure)

3. **Document References**: When you mention "mirroring" content instead of redefining it, are you thinking of:
   - Automatic content inclusion/references (like markdown includes)? (No)
   - Manual linking between sections? (No)
   - A more sophisticated content relationship system? (Yes)

- The structure will be built up via a JSON reference table where each element will be either a parent, peer or child of another element.
- All elements will have unique ids which will be how the structure know what to put where
- I i discribe the stall using sentences (ELEMENTS), then these create a unique id for the paragraph (COMPONENT) and I add some more images and captions (COMPONENTS) and put them all together to create a SECTION. The section have a UUID, The components will have UUID and the ELEMENTS will have UUID so the whole tree will be a JSON structure of nested UUIDs

## User Experience Questions

4. **Editing Workflow**: When editors make changes, should they:
   - Edit directly in a WYSIWYG interface? (YES)
   - Work with markdown/structured text? (NO)
   - Use a form-based editor for the atomic components? (NO)

- When an editor wants to edit, they should activate an edit mode. This then allows them to edit the document freely.
  - Add text, update text, remove or add images etc...
- The WYSIWYG editor should have basic controls ar the top similar to MS Word, but just for the aspects you can control on a markdown file
- Once they are done, they will click submit and essentially a pull request will be sent to the managers for approval.
- The editor will have a page where they can see their pending edits. (The can be done in a github diff red minus and green plus style)
  - This page will also show a history of approved and rejected edits.
  - A rejected edit will have a section that shows why the edit was rejected

5. **Approval Process**: How granular should approvals be?

   - Can managers approve individual elements (sentences, images)?
     (Yes via an individual checkbox then click approve)
   - Must entire sections be approved together?
     (This can be done via a checkbox select all and then click approve)
   - Should there be partial approval capabilities?
     (Already answered)

6. **Notification Preferences**: Should users be able to:
   - Subscribe to specific topics/tags? (No)
   - Set notification frequency (immediate, daily digest, weekly)? (No, they get the notification as the activity happens)
   - Choose notification channels (email, in-app, SMS)? (Only in-app, this will be a web-app)

## Content Structure Questions

7. **Content Relationships**: Beyond the atomic structure (elements � components � sections), how should we handle:

   - Cross-references between sections?
   - Explain more what you mean by this

   - Dependencies (e.g., "Section A must be read before Section B")?
   - Explain more what you mean by this

   - Version compatibility between related sections?
   - Versions will be controlled by a total document checksum after each merge.
   - This will also be used to sync the version control. So if you have a chache version on your device it will reference the checksum, if this fails it goes to the last checksum that passed and then syncs only those diffs instead of syncing the whole document. This can be fleshed out in more detail

8. **Document Hierarchy**: Above sections, what's the top-level organization?
   - Documents � Sections � Components � Elements? (Yes)
   - Categories/Modules � Documents � Sections? (No)
   - Something else? (No)

## Aviation-Specific Questions

9. **Regulatory Compliance**: Are there specific aviation documentation standards we need to consider?

   - CAA/FAA formatting requirements? (No - This should be built to be company/industry agnostic for now)
   - Audit trails for regulatory inspections? (No)
   - Required approval workflows for safety-critical information? (No - Keep it simple, editors/managers edit and managers approve/reject with an audit trail on changes made, by who and who approved or rejected those changes)

10. **Content Types**: Are there aviation-specific content types we should plan for?
    - Checklists with specific formatting? (Not for now)
    - Weather minimums tables? (No)
    - Aircraft-specific procedures? (No - but there can be a type of list item element that is a checklist item so challenge response type FLAPS ... LAND)
    - Emergency procedures with special highlighting? (No, but text color and background color can be added)

## Scalability & Performance

11. **Multi-School Usage**: If this expands beyond your flying school:

    - Should schools have isolated document sets? (This will only be used inhouse and docs won't be shared to other companies)
    - Any shared industry-standard content? (No)
    - How to handle different aircraft types/regulations? (No)

12. **Offline Access**: Should the system work offline for:
    - Students studying without internet?
      - There should be the ability to handle the whole app offline (Using service workers) or at least make certain sections available offline.
      - The version will be controlled via a checksum of the whole document. If the versions are not the latest there should be a clear flag and the options to sync the diffs from the last correct checksum until the latest version
    - Instructors in aircraft without connectivity? (Won't be used in flight at all)
    - Emergency procedure access? (Will not be referenced for any emergency)

---

## Next Round of Questions - Technical Implementation Details

Based on the projectSpecs.md, here are deeper technical questions that need clarification:

### UUID & Content Management

13. **UUID Scope & Collision**: How should UUID generation work?

    - Generated client-side or server-side?
      - Client side geenration can be done each time an element is added or edited as an edited element will have a different UUID compared to it's original
    - What happens if two editors create content simultaneously?
      - When they submit, it will show as two seperate pull requests, the manager will decide which to merge
      - The manage should be able to see then in chronological order and decide how to approve them
    - Should UUIDs be human-readable in any way for debugging?
      - No, they can be standard style UUIDs, but there should be a section where you can see the element, component or section based on a UUID (Essentially a UUID lookup)

14. **Content Reuse Mechanics**: When an element is referenced in multiple places:

    - How does editing work? (Edit source and all references update?)
      - When you edit the element it's essentially change as the source of truth, all references to this is then also pointing to the new source of truth
      - The structure of how this happens should be fleshed out as if an element is referenced by a lot of other components/sections, this could couse a complex sequence of updates and modifications.
      - So maybe the refernce can be done on a certain section of the UUID and the version of that element can be controlled by a differenct section of the UUID
    - Can references have different styling/context?
      - Not sure what you mean by this, ellaborate on the question
    - What happens if someone tries to edit a referenced element?
      - The edit will take place on that single source of truth and the refernce is updated to point to this new updated single source of truth

15. **JSON Structure Storage**: Where and how is the JSON tree stored?
    - As part of git repository in special files?
      - There will be a data layer
      - For now this can maybe just be mocked using local storage
      - Some of the docs could be restricted information, so online storage could be questionable and maybe a self hosted supabase would work. But this can be explored later
    - Separate database alongside git?
      - As discussed above
    - How do you handle large documents with thousands of UUIDs?
      We'll have to find a way to manage this still, I'm not sure

### Git Integration Details

16. **Branch Management**: For the username-based branches:

    - What if a user has multiple pending edits?
      - Just use the username datestamp layout Jake202509161212 (UsernameYYYYMMDDHHSS )
    - How do you handle branch naming conflicts (special characters in usernames)?
      - This should not be an issue using the above mentioned method
    - When are branches cleaned up after merge/rejection?
      - They are not essentially branches, they will more be stored as diffs linked to the master branch, so instead of thinking about it as a completed branch, it's more a diff off of the master branch

17. **Merge Conflicts**: What happens when:

    - Two editors modify the same element simultaneously?
      - When they submit the pull request of the diffs the manager will see them in chronoligical order and then select which one he wants to work on first, after he has merged the one, he can start with the second one as if they were sent days after eachother, this will be an edgecase to have changes so close together on the same elements
    - Manager approves one change but another editor has a pending change to same content?
      - The changes the manager approves are merged, then if the next changes reference the old version it can simply show how it would fit into the newly merged content
    - Git merge conflicts occur at the technical level?
      - I'm not sure what you mean, elaborate more on this question

18. **Git Repository Structure**: How should the repo be organized?
    - Separate files per document/section/component?
      - For now it can just be one monorepo (large) style document
    - Single large JSON file with all content?
      - Yes
    - Mix of content files + structure files?
      - No - The idea is to have a single source of truth that does not get damaged

### WYSIWYG Editor Integration

19. **Editor Boundaries**: In edit mode:

    - Can users edit across section boundaries?
      - Not sure what you mean by this
      - A user edits the elements of a section/component and these elements are presented as diffs for the manager to apporve or deny
      - Multiple sections and components can reference the same element, but where this element is changed, all the references change to the new element
        - An example of this would be where the take off is discribed. Some elements of this description will be used for various types of take offs, if the single source of truth for how to power up for the take off is changed, then all the components that referenced this element of how to power up for the take off will be updated to point to the new reference for the take off
    - How do you prevent users from breaking the atomic structure?
      - There is always only one single source of truth
      - The web-app must manage the atomic structure
    - What happens if someone deletes a UUID reference accidentally?
      - Users will not have access to edit or delete UUID refernces or change anything on the reference tree, this will all be system controlled

20. **Real-time Collaboration**: While editing:
    - Can multiple editors work on same document simultaneously?
      - Essentially the whole app is a single document
      - Users draw data from the server and send edits to the server, but there is no need to build in realtime collaboration
    - How do you handle live updates and conflicts?
      - As discussed above
    - Should there be locking mechanisms?
      - No

### Data Consistency & Performance

21. **Checksum Calculation**: For version control:

    - What level of granularity for checksums (document, section, element)?
      - Good enough to make sure versions are up to date
    - How often are checksums calculated?
      - There can be a TTL of 7 days and a "check version" prompt from the user to run the checksum, then compare it to the online (source of truth version)
    - What's included in checksum calculation (content + structure + metadata)?
      - Whatever is needed to manage the checksum properly. UUIDs should be good enough

22. **Offline Sync Edge Cases**: When coming back online:
    - What if local changes conflict with approved changes made while offline?
      - The changes should only be able to be merged when there is an internet connection
    - How do you handle partial sync failures?
      - No offline merge
    - Should there be a "sync queue" for offline actions?
      - No

### User Experience Edge Cases

23. **Approval Workflow Edge Cases**:

    - Can an editor cancel their own pending changes?
      - Yes
    - What if a manager wants to edit someone else's pending change before approval?
      - They can approve the edit, then edit it as their own edit, this keeps the app more simple
    - Should there be a "request changes" option (like GitHub) vs just approve/reject?
      - No, essentially the reject with a message is a request changes request

24. **Content Dependencies**: If Element A references Element B:
    - What happens if Element B gets rejected while Element A is pending?
      - The ****************\*\*****************
      ***
    - How do you visualize these dependencies to managers during approval?
    - Should changes to referenced content trigger re-review of dependent content?

### Search & Tag Architecture

25. **Tag Management**: For the manual tagging system:

    - Who can create new tags vs use existing ones?
    - How do you prevent tag proliferation/inconsistency?
    - Should there be tag synonyms or tag hierarchies?

26. **Search Performance**: For complex tag-based searches:
    - How do you index tagged content for fast search?
    - What happens when searching across thousands of documents?
    - Should search results show context (surrounding paragraphs)?

### Authentication & Security

27. **User Management**: How should user accounts work?

    - Integration with existing company systems (LDAP, etc.)?
    - Role assignment mechanism?
    - User account lifecycle (deactivation, role changes)?

28. **Data Security**: For document content:
    - Should there be audit logs beyond git history?
    - Any encryption requirements for sensitive content?
    - How to handle data retention policies?

Please review and answer the questions that are most critical for moving forward with the technical design!
