# playbook_demo

This Repo is linked with Automation Playbook hosted at gitbook.io

## How to Contribute:

As the playbook is meant to be updated based on learnings of the team, it is essential to provide an entry point to contributing towards keeping it latest.

**_NOTE_**:Only changes published to master branch will be 
In order to contribute you would need to use the following process.

- Download [Git-SCM](https://git-scm.com/downloads)
- Clone this repository 
  ```bash
  git clone https://github.com/asimkazmi/playbook_demo.git
  ```
- Create a branch 
  ```bash
  git checkout -b feature_branch_name
  ```
- Add your changes to the existing page, or add a new page. 
  - If you would like to add any images to your updates, put them in _/pages/attachments/[your image file name>]_
  - Reference your images on the document as:
    ```
    ![Reference Name](attachments/[your image file name>])
    ```
- Update /pages/SUMMARY.md to add TOC reference to your content file

- Once you are satisfied with all changes you want to update, push your code to remote branch 
    ```bash
    git push -u origin feature_branch_name
    ```
- Create a pull request to merge your branch on master
- Assign Reviewers to it (Any one from the team can review but only Automation Guild Core Group can merge to master)
- If there is review feedback, work on it and push to your branch so that it can be added to your pull request automatically. 
- Once approved, your branch will be merged to master and the changes will be published on Gitbook. 
___
## Folder Structure: 
```txt
/root
    book.json
        - Git Book congfiguration File - DO NOT UPDATE
    README.md 
        - Readme file for this repository
    .gitignore
        - File used by git to ignore managing files from on your local  repository being pushed to remote.
    /pages
        - All Content Files 
        /attachments 
            - All attachments for the content pages
            - Supported File Types: JPEG, PNG, PDF, PPTX, MOV etc. 
        /images
            - Images required by gitbook theme 
        /_book
            - Folder created by gitbook package to host and view contents locally. 
```    
___
## How to View Contents in Git book style locally

If you want to view how your content looks before publishing it to github repository, you can do installing the npm gitbook package. 
```
npm install 
```
- go to /pages folder
  - Create the directories and files for a book from its SUMMARY.md file
    ```
    gitbook init
    ```
  - To serve a repository as a book
    ```
    gitbook serve
    ``` 
  - To build the static website
    ```
    gitbook build
    ```