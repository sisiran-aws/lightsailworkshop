+++
title = "Web extension"
weight = 4
+++

Now that you have deployed your bookmarking app, you can setup the web extension to save links as you browse.

Before you begin, create an account on your deployed linksaver app and remember your password.

{{% notice info %}}
This extension has only been tested on Chromium based browsers such as Chrome and Brave.
{{% /notice %}}

### Setup

1. Open your browser and navigate to the extensions page. This is usually available under settings > extensions.
2. On the extensions page, make sure _Developer mode_ is **enabled**.
3. Choose _Load unpacked_.
4. Navigate to the location where your saved the linksaver repo and select the `webext` directory.
5. In the toolbar, under the extensions icon, choose new _Linksaver_ extension.
6. A setting page will open up. Enter the URL of your new container service and choose _Save_.
7. Choose _Login_ and enter your email address and password.
8. Now you should be able to save bookmarks as you browse by clicking the _Linksaver_ extension in your toolbar.

The extension's settings page should look something like this:

![linksaver extension settings page](../../images/linksaver-ext-settings.png)

When you save links with the extension, you should see a green check emoji like this:

![saving a link wit the linksaver extension](../../images/linksaver-ext-saving.png)
