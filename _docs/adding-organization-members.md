---
layout: docs
title: Adding Organization Members
---

Once you have [created your organization](% link _docs/create-an-organization.md %}), you can get started by adding members to it.

As opposed to personal apps, apps in an organization do not have app members. Members in an organization have access to all the apps in it. And you can manage members roles across all the apps in an organization.

Let's start by adding members.

From the settings screen of your organization, view the members that are a part of it.

![Organization settings](/assets/docs/adding-organization-members/organization-settings.png)

Here you'll be able to add new members.

![Organization members](/assets/docs/adding-organization-members/organization-members.png)

### Adding Members

Add a member to the organization using their email address.

![Add member form](/assets/docs/adding-organization-members/add-member-form.png)

If you are adding a member that doesn't have a Seed account, they'll be asked to create one with the email address that you specify.

You can also assign them a role while adding them to the organization.

### Member Roles

There are a few different member roles in Seed. Let's take a quick look at them.

| Role           | Description |
|----------------|-------------|
| Admin          | Admin members have access to all aspects of the organization. They can add or remove apps, stages, and services. They can add or remove any member of the organization. And they also have access to billing. |
| Deploy Dev     | Members can only manage and deploy to development stages in the apps that are a part of the organization. |
| Deploy Staging | Members can manage and deploy to staging and dev stages in the apps that are a part of the organization. |
| Deploy Prod    | Members can manage and deploy to production, dev, and staging stages in the apps that are a part of the organization. |
|----------------|------------|

>> Allowing a member to deploy to dev, staging, and prod is not the same as granting them admin access.

Also note that by granting _Deploy Prod_ access, forces you to grant them _Deploy Dev_ and _Deploy Staging_ access. And granting _Deploy Staging_ access automatically enables _Deploy Dev_ access.

### Changing Roles

Once a member has been invited or added to the organization, you can still go in and change their roles.

![Edit member roles](/assets/docs/adding-organization-members/edit-member-roles.png)

Finally, you can remove a member from an organization and they will no longer have access to the apps in the organization.
