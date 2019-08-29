---
layout: docs
title: Adding an SSH Key for Your Organization
---

You can set a private SSH key that Seed will use for all the build processes in your organization. There are a couple of reasons why you might want to do this:

1. To check out any additional Git repositories as a part of your build process.
2. To run any other operations involving SSH (ie, rsync, ssh, etc.)

To run the above operations you'll need your private SSH keys in the build process.

> Make sure to not store your private SSH keys in your seed.yml or repo.

You can set this by adding a private SSH key for your organization.

### Adding an SSH Key

Head over to your organization settings and click on **Add Org SSH Key**.

![Org setting SSH key](/assets/docs/adding-an-organization-ssh-key/org-setting-ssh-key.png)

Enter your private key and hit **Add**.

![Enter private SSH key](/assets/docs/adding-an-organization-ssh-key/enter-private-ssh-key.png)

Once it has been added, double check that it has been set correctly by comparing the displayed fingerprint.

![View SSH key fingerprint](/assets/docs/adding-an-organization-ssh-key/view-ssh-key-fingerprint.png)

### Check out Other Repos

If you are looking to check out other repositories as a part of your build process, make sure that you are using the correct SSH URL format:

- GitHub: `git@github.com/...`
- BitBucket: `git@bitbucket.org/...`
- GitLab: `git@gitlab.com/...`

### Behind the Scenes

Here is what Seed does when an SSH key has been set.

1. Takes the private key and writes it to the `~/.ssh/id_rsa` file when the build process starts.
2. Changes the file permissions to `600`.
3. Adds the Git providers domain to the known hosts. Seed uses the same Git provider as the one being used in the build process. For example, if your app is tied to GitHub, then GitHub will be added to the known hosts.

Note that, the SSH key is used in _all_ the build processes for _all_ your apps in your organization.
