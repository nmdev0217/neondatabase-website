---
title: Get started with branching
enableTableOfContents: true
isDraft: false
---

This topic describes how to get started with Neon's branching feature, which allows you to branch your data in the same way that you branch your code.

A branch is a clone of your data that you are free to play around with and modify without affecting the originating data.
For more information about what branches are and how to use them in your development workflows, see [Branching](../../conceptual-guides/branching).

<Admonition type="note">
Neon Branching capabilities are not yet publicly available. If you would like to try this feature, reach out to [iwantbranching@neon.tech](mailto:iwantbranching@neon.tech) describing your use case and requesting that Neon enable branching for your account.
</Admonition>

You can create and manage branches using the Neon Console or Neon API. In this topic, we cover branching using the Neon Console.

Before you can create a branch, you must have a Neon project. If you do not have a Neon project, see [Setting up a project](../setting-up-a-project).

## Create a branch

To create a branch:

1. In the Neon Console, select a project.
2. Select **Branches**.
3. Click **New Branch** to open the branch creation dialog.
![Create branch dialog](./images/create_branch.png)
4. Enter a name for the branch.
5. Select a parent branch. You can branch from your Neon project's [root branch](../../reference/glossary/#root-branch) (`main`) or a previously created branch. Every Neon project is created with a root branch called `main`.  
6. Select one of the following branching options:
    - **Head**: Creates a branch with data up to the current point in time (the default).
    - **Time**: Creates a branch with data up to the specified date and time.
    - **LSN**: Creates a branch with data up to the specified [Log Sequence Number (LSN)](../../reference/glossary/#lsn).
7. Click **Create Branch** to create your branch.

You are directed to the **Branches** page where you are shown the details for your new branch.

## View branches

To view the branches in a Neon project:

1. In the Neon Console, select a project.
2. Select **Branches** to view the branches for the project.
3. Select a branch from the table to view details about the branch, including the branch's endpoint hostname.

![Branch details](./images/branch_details.png)

<Admonition type="note">
Each branch is created with an endpoint, which is the compute instance associated with the branch. To connect to a branch, you must connect to the endpoint. For instructions, see [Connect to a branch](#connect-to-a-branch). A endpoint hostname starts with an `ep-` prefix. You can also find an endpoint hostname in the branch connection string in the **Connection Details** widget on the project **Dashboard**.
</Admonition>

The **Branches** widget on the project **Dashboard** also lists the branches in a Neon project. Selecting **Manage** from the **Branches** widget directs you to the **Branches** page, where you can view and manage branches.

## Connect to a branch

Connecting to a branch requires connecting to the branch's endpoint, which is the compute instance associated with a branch. The following steps describe how to connect to a branch using `psql` and a connection string obtained from the Neon Console.

<Admonition type="tip">
You can also query a branch from the Neon SQL Editor. For instructions, see [Query with Neon's SQL Editor](../query-with-neon-sql-editor).
</Admonition>

1. In the Neon Console, select a project.
2. On the project **Dashboard**, under **Connection Details**, select the branch, the database, and the user you want to connect with.
![Connection details widget](./images/connection_details.png)
3. Copy the connection string. A connection string includes your user name, the endpoint hostname, and database name. The endpoint is the compute instance associated with the branch.
5. Add your password to the connection string as shown below, and connect with `psql`. You can connect using the same user and password that you use to connect to the parent branch.

  ```bash
  psql postgres://casey:<password>@ep-polished-water-579720.us-east-2.aws.neon.tech/main
  ```

<Admonition type="tip">
The endpoint hostname, which is `ep-polished-water-579720.us-east-2.aws.neon.tech` in the example above, can also be found on the **Branches** page in the Neon Console. For instructions, see [View branches](#view-branches).
</Admonition>

If you want to connect to a branch from an application, the **Connection Details** widget on the project **Dashboard** also provides connection examples for various languages and frameworks.

## Delete a branch

Deleting a branch is a permanent action. Deleting a branch also deletes the branch endpoint, which is the compute instance associated with the branch. You cannot delete a branch that has child branches. The child branches must be deleted first.

To delete a branch:

1. In the Neon Console, select a project.
2. Select **Branches**.
3. Select a branch from the table.
3. Click **Delete**.
4. On the **Delete the branch?** dialog, click **Delete**.
