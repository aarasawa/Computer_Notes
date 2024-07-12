#pre-commit #testcases #OpenLibrary #OpenSource 

If a commit adds, removes, or alters text visible to an end-user and is properly *internationalized*, an update of the translation template file with auto-bundle with changes.

Since you're running pre-commit locally:
1. Code will fail **Generate POT**, throw error **Files were modified by this hook**, and add **messages.pot** to unstaged changes in git
2. To pass, add messages.pot file to staging and redo commit. Generate POT should pass now. 