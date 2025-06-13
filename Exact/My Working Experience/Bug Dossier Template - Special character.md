# Bug Copy To Existing Dossier

**Work item description**
- Hit Oops error page when user try to copy folder
- Reason: folder name contains slash (/)
- User's (/) and system's (/) are mixed together
- i.e. user's folder: "png/pdf"; path: "Receipts / png/pdf"
- Guess how many folders? system said 3, but it is 2. 

**This sprint took 4 weeks to settle 💩**
- Really bad.... I was tried to refactor all logic flow inside the "CopyFolders" function.
- Rejected by senior, difficult for reviewing
- The function was not well tested previously
- No enough covering alternative & exceptional flow

**About the "Copy to existing dossier"** 🤓
- If user account has SharePoint connection setting, this function run in one single on demand background task, else run one for each division.  
- If selected folders already exist in dossier, do not copy
- then, if folders has no parent, copy without parent ID, else with.
- then, copy "document type" value to dossier. (not stable 💩)
- Very bad one: `folder.ID = newCreatedFolderId` is updating reference, which will used by another function later. It is super confusing 😵‍💫 and inconsistent.  

**Wrap up**
- Focus on the root cause 💣, not the code 🛠️. 
- Create new tech debt📝 immediately for refactoring if really messy.
- Create new bug 💣 if different Oops found.  

