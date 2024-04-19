## Description of branch types

Commit should be done according with the following instructions.
If for some reason we push straight to the main branch (Develop)
commits should look like below.

**commit message:** `feat: added a new method to delete users` 
# todo add information about commits name convention

if we create a branch based on some user-story.  

**branch name:** `feat/20-add-new-a-new-method-to-delete-users`  

### List of All Acceptable Branch Types

| Branch Type | Description                                                                     |
|-------------|---------------------------------------------------------------------------------|
| feat/       | A new feature based on an issue, user story, or task.                           |
| bugfix/     | A bug fix for the develop branch.                                               |
| rf/         | Refactor, simplifying code, code formatting, white-space, missing semi-colons. |
| doc/        | Documentation updates, markdowns, or in-code documentation.                      |
| test/       | New unit tests, integration tests, performance tests, or correcting previous tests. |
| chore/      | Dependency version bump.                                                         |
| devops/     | CI/CD, GitHub Actions, workflows, issue templates, build.yaml, Dockerfile, etc. |


**ofitoo-doc** is exempt from adding any branch-type due to the nature of the repository,  
everything is **doc/** by default so there is no point in adding it.