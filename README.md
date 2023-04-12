
# Apple PKPass

Apple Wallet Developer Guide

# Building Your First Pass

In this tutorial, you download and edit a sample pass, build it, and view it in the iOS Simulator app.



## Creating and Populating the Pass Package

Passes are created as a package (also referred to as a bundle) containing a pass.json file that defines the pass, and image assets such as the logo and the icon.

To create the pass package for your pass, do the following:

1. Make a new directory in the Documents folder called Lollipop.pass. Using the .pass extension is a best practice, showing that the directory is a pass package.

2. Download this book’s companion file (from the developer downloads area), and locate the coupon in the Sample Passes directory.

3. Open the raw pass package, and copy the files it contains to your Lollipop.pass directory.

## Setting the Pass Type Identifier and Team ID
 
Every pass has a pass type identifier associated with a developer account. Pass type identifiers are managed in Member Center by a team admin. To build this pass, request and configure a pass type identifier. (You can’t use the pass type identifier that is already in the pass because it isn’t associated with your developer account.)

To register a pass type identifier, do the following:

In Certificates, Identifiers & Profiles, select Identifiers.

Under Identifiers, select Pass Type IDs.

Click the plus (+) button.

Enter the description and pass type identifier, and click Submit.

To find your Team ID, do the following:

Open Keychain Access, and select your certificate.

Select File > Get Info, and find the Organizational Unit section under Details. This is your Team ID.

The pass type identifier appears in the certificate under the User ID section.

NOTE

You can also find your Team ID by looking at your organization profile in Member Center.

Edit the pass.json file, and change the pass type identifier to the identifier you just set up. Then change the Team ID to match the values you just found (see Listing 3-1).

Listing 3-1Setting the pass type ID and Team ID
{
    ...
    "passTypeIdentifier" : "
your pass type identifier
",
    "teamIdentifier" : "
your Team ID
",
    ...
}


## Signing and Compressing the Pass

As part of building your production environment, you will need to set up a system for automatically signing and compressing passes as described in Passes Are Cryptographically Signed and Compressed. For this tutorial, a very simple tool for signing passes is included.

To download your pass signing certificate, do the following:

In Certificates, Identifiers & Profiles, select Identifiers.

Under Identifiers, select Pass Type IDs.

Select the pass type identifier, then click Edit.

If there is a certificate listed under Production Certificates, click the Download button next to it.

If there are no certificates listed, click the Create Certificate button, then follow the instructions to create a pass signing certificate.

To get the signpass tool, do the following:

Download this book’s companion file (from the developer downloads area), and locate the signpass project.

Open the project in Xcode, and build it.

Right-click on the signpass executable (in the Products folder in Xcode) and select Show in Finder.

Move the signpass executable to the Documents folder.

To sign and compress the pass, use the signpass tool to sign the pass package. In Terminal, run the following commands:

```bash
cd ~/Desktop
./signpass -p apple_pass.pass
```


These commands create a signed and compressed pass named Lollipop.pkpass in the Documents folder. If the signpass command fails, make sure you are using your correct pass type identifier and check that the pass.json file contains valid JSON.

