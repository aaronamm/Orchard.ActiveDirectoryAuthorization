# Active Directory Authorization for Orchard

[Orchard](http://www.orchardproject.net/) is a community driven content management system that allows users to rapidly create websites for the .NET platform. This module overrides the default authentication & authorization by using the currently logged in active directory user instead of requiring a user to authenticate using credentials.

## How it works

This [blog post](http://peterkeating.co.uk/active-directory-authorization-module-for-orchard/) contains more detail about why we built the module and how it works.

## Status

An update (v1.2) is now [available from the Orchard Gallery](https://gallery.orchardproject.net/List/Modules/Orchard.Module.ActiveDirectoryAuthorization) to solve issues with Orchard 1.8.x.

## Versions

### 1.3.

* Reduce needless database hits by storing user as private variable.
* Compatible as a git submodule.
* Compatible with Orchard v1.10.x.

### 1.2

* Fixed stack overflow exception caused by dependency to `IMembershipService`.
* Updated project to target .NET 4.5.
* Removed call to the method that has been removed (`ContentManager.Flush`).

[Published on 7th March 2015](http://gallery.orchardproject.net/List/Modules/Orchard.Module.ActiveDirectoryAuthorization/1.2)

### 1.1

* Fixed bug with active directory users having multiple Orchard users created.
* Active directory users have an orchard user created for them no matter what role they have, instead of only being created when the user has access to the Admin dashboard.
* Email address of the active directory user is saved on the Orchard user that is created.
* Roles set on Orchard users in the administration area are now taken into account as well as AD user roles when checking user access to a permission.
* Fixed bug with null reference exceptions occurring when the User on the context is null.
* Fixed bug causing exception when the content item permission part is enabled on a content item.
* Active directory user roles are checked against orchard roles, any matched roles are assigned to the orchard user that is created on active directory user's first visit.

[Published on 3rd April 2013](http://gallery.orchardproject.net/List/Modules/Orchard.Module.ActiveDirectoryAuthorization/1.1)

### 1.0

*Original Release.*

[Published on 17th October 2012](http://gallery.orchardproject.net/List/Modules/Orchard.Module.ActiveDirectoryAuthorization/1.0)

## Installation

In order to install the module follow the steps below.

1. Add the relevant roles in Orchard that your Active Directory users have. It is important that the name of the Orchard role matches the name of the role in your active directory. For example "MyDomain\MyContentManagerRole" should be both an AD and Orchard role.

2. In the modules section in the administration dashboard for your Orchard install search the gallery for **Active Directory Authorization** and then download the module titled **Active Directory Authorization**. Ensure that you have completed the first step of adding the roles before you enable the module otherwise you may lock yourself out of the administration dashboard. If you have any problems installing the module through the Orchard Gallery then alternatively you can download and install this module manually following the instructions below.
   * Download the latest .nupkg from the downloads section of this repository.
   * Install the module into your instance of Orchard follow the instructions for [installing a module from your local computer](https://github.com/OrchardCMS/OrchardDoc/blob/master/Documentation/Installing-and-upgrading-modules.markdown#installing-a-module-from-your-local-computer).<br /><br />

3. Once the module is installed and enabled, you need to setup IIS to enable windows authentication.
	On IIS7 and newer, open IIS and navigate to your Orchard website. Select the "Authentication" option, then enable "Windows Authentication", and have the rest as disabled.

4. The final step is to change the authentication configuration in the Web.config of the root of your website, replacing the current configuration to use FormsAuthentication.
	<pre><code>&lt;authentication mode="Windows" /&gt;
	&lt;roleManager enabled="true" defaultProvider="AspNetWindowsTokenRoleProvider"/&gt;
	</code></pre>
