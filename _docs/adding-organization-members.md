---
layout: docs
title: Adding Organization Members
---

Once you have [created your organization](% link _docs/create-an-organization.md %}), you can get started by adding members to it.

As opposed to personal apps, apps in an organization do not have app members. Members in an organization have access to all the apps in it. And you can manage members roles across all the apps in an organization.

Let's start by adding members.

From the **Members** tab of your organization, you'll be able to add new members.

![Organization members](/assets/docs/adding-organization-members/organization-members.png)

### Adding Members

Add a member to the organization using their email address.

![Adding new member to Seed](/assets/docs/adding-organization-members/adding-a-new-member-to-seed.png)

If you are adding a member that doesn't have a Seed account, they'll be asked to create one **with the email address that you specify**.

You can also hit **Edit** to change the role that is assigned to them.

![Fine-grained rbac in Seed](/assets/docs/adding-organization-members/fine-grained-rbac-in-seed.png)

### App Specific Roles

By default the member role applies to the entire organization. But you can modify the role for specific apps in your org. Use the **Add a specific role for an app** dropdown to select the app you want.

![Select app for app specific role in Seed](/assets/docs/adding-organization-members/select-app-for-app-specific-role-in-seed.png)

And hit **Add**.

![Click add for app specific role in Seed](/assets/docs/adding-organization-members/click-add-for-app-specific-role-in-seed.png)

Here you can modify the role you'd like to assign for this specific app.

![Select role for app specific role in Seed](/assets/docs/adding-organization-members/select-role-for-app-specific-role-in-seed.png)

Once selected, the app specific role **overrrides** the org role assigned.

![App specific role selected in Seed](/assets/docs/adding-organization-members/app-specific-role-selected-in-seed.png)

So for this example, the **Admin** role applies for the entire org and all the apps, except for the **my-serverless-app** app.

### Member Roles

There are a few different member roles in Seed. Let's take a quick look at them.

| Role           | Description |
|----------------|-------------|
| Admin   | Admin members have access to all aspects of the organization. They can add or remove apps, stages, and services. They can add or remove any member of the organization. And they also have access to billing. |
| Dev     | Members can manage, deploy, and promote to the development stages in the apps that are a part of the organization. |
| Staging | Members can manage, deploy, and promote to the staging stages in the apps that are a part of the organization. |
| Prod    | Members can manage, deploy, and promote to the production stages in the apps that are a part of the organization. |
| Billing | Members have the ability to update the billing settings of the organization. |
|----------------|------------|

>> Allowing a member to deploy to dev, staging, and prod is not the same as granting them admin access.

Note that if a member is _only_ granted the billing role, they are only allowed to manage the billing settings of the organization.

#### Fine-Grained Roles

For the **Dev**, **Staging**, and **Prod** roles, you can further restrict access by selecting the following:

- **Manage**: Members have access to the settings of a stage.
- **Deploy**: Members can manually deploy to the stage.
- **Promote**: Members can promote to the stage.

Note that, **Promote** access refers to the ability to promote **to the stage** in question. For example, if a member has promote access to the staging stages; this means that they can promote to staging.

And since you cannot promote _to_ development stages, there is no promote role for Dev.

### Changing Roles

Once a member has been invited or added to the organization, you still have the ability to go in and change their roles by hitting the **Manage** button.

![Edit member roles](/assets/docs/adding-organization-members/edit-member-roles.png)

Finally, you can remove a member from an organization and they will no longer have access to the apps in the organization.
