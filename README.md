# Paperpile to Notion Sync Tool

A simple tool to automatically sync your Paperpile library with a Notion database.

## Notion Setup

1. Create a new page (e.g. "Papers").
2. On your page, add a new Table view.
3. Select "New table" in the New view dropdown, and name it something sensible, e.g. "Paperpile." 
5. Delete any empty rows from the table, and modify it so it has at minimum the following properties:

    1. `Reference ID` of type Title.
    2. `Title` of type Text.
    3. `Authors` of type Text.
    4. `Year` of type Text.
    5. `Link` of type URL.

6. Get the **database identifier** from the database page. If your database url is:

    ```
    https://www.notion.so/my_workspace/aaaabbbbccccddddeeeeffffgggghhhh?v=iiiiiiijjjjkkkkllll
    ```

    Then the database identifier is: `aaaabbbbccccddddeeeeffffgggghhhh`. The string starting with `?v=` refers to a specific view of the database, and can be omitted.

7. Create a new integration on [https://www.notion.so/my-integrations/](https://www.notion.so/my-integrations/).

    1. Name: Paperpile to Notion
    2. Associated Workspace: Workspace of the database.
    3. Content Capabilities: Read Content, Update Content, Insert Content.
    4. User Capabilities: Read user information, including email addresses.
    5. Press "Submit" and copy the **Internal Integration Token**.

8. On the database page, click "Share" (top right) and add "Paperpile to Notion" with edit access.

## GitHub Setup

1. Fork this repository.
2. On your fork, go to: "Settings -> Secrets and variables -> Actions".
3. Create 2 new repository secrets named exactly:
    
    1. `NOTION_TOKEN`: Your integration's internal integration token, from step 3.5 above.
    2. `DATABASE_IDENTIFIER`: Your database identifier, from step 2 above.


## Paperpile Setup

1. Click on the top-right gear icon, and go to "Workflows and Integrations".
2. Follow the instructions to add a new "BibTeX Export", choosing:

    1. Your GitHub repository fork as the repository. You can find the details under "Code -> Local -> Clone -> SSH."
    2. `references.bib` as the export path.

The first sync should start as soon as the Paperpile workflow is created, and subsequent syncs are triggered whenever papers are added or updated in your Paperpile.

**Note**
The first sync might take some time as Notion limits the API rate to ~ 3 requests / second; so if you have 1,000 papers it'll take ~ 6 minutes before they are all available in Notion.

---

Forked from [apoorvkh/paperpile-to-notion](https://github.com/apoorvkh/paperpile-to-notion), which in turn was rewritten from [seba-1511/sync-paperpile-notion](https://github.com/seba-1511/sync-paperpile-notion). 
