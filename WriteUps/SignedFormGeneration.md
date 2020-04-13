# Signed Form Generation from Word Templates
This write up was put together on 4/13/2020.

This example builds on the Electronic Signatures Demo app [Electronic Signatures Demo App](./ElectronicSignatures.md).  This explains how you can capture an electronic signature in a canvas app and then populate that into a Word template and create a PDF of the signed form.  

![Final Result](Images/signed-form-PDF-result.JPG)

## Power Automate Flow Overview
Here is an outline of how you can accopmlish this using the data from the [Electronic Signatures Demo App](./ElectronicSignatures.md).  This Flow is triggered when a new Signature CDS record is created.  The signature image is downloaded, and then it is populated into a Word template file which is then exported to a PDF and sent to an email address.

![Flow Overview](Images/signed-form-flow-overview.JPG)

## Word Templates Overview
Word templates with control types have been around for many years.  You can use them to standarize reports for your organization. Below is a link to read more about them,

https://support.office.com/en-us/article/create-forms-that-users-complete-or-print-in-word-040c5cc1-e309-445b-94ac-542f732c8c8b?ui=en-US&rs=en-US&ad=US

Power Apps and Dyanmics support Word Template files to create reports off of entities in CDS.  To date, those templates do not support image control types in Word templates.  

https://docs.microsoft.com/en-us/power-platform/admin/using-word-templates-dynamics-365

So for this example, we cannot use that feature.  Instead, we will use the [Word Online (Business) connector](https://docs.microsoft.com/en-us/connectors/wordonlinebusiness/).  This connector has support for many of the content control types that you can create in Word.

https://docs.microsoft.com/en-us/connectors/wordonlinebusiness/#currently-supported-content-controls

## Setup
Create a Word template as described above.  Next, add the template file to a location in your OneDrive for Business account.  Lastly, make sure you have the [Electronic Signatures Demo App](./ElectronicSignatures.md) running in your environment.

## Creating the Flow

### Trigger
Create a new Flow with the trigger using the [Common Data Service](https://docs.microsoft.com/en-us/Connectors/commondataserviceforapps/#when-a-record-is-created,-updated-or-deleted) connector when a new Signature entity is created.

![Trigger](Images/signed-form-trigger.JPG)

### Get Created By User Name
Add a new action to get the display name of the user who created the entity.  This is using the [Common Data Service](https://docs.microsoft.com/en-us/Connectors/commondataserviceforapps/#get-a-record) connector to get a record.

![Get User Info](Images/signed-form-get-user-info.JPG)

### Store the Base OData URL
The Common Data Service exposes its data over REST with an OData endpoint.  The URL for each environment is unique.  You could hardcode this URL for your Flow, but I chose to make my Flow dynamic for any environment.  Here I parse the results of the previous "Get a Record" action and parse the @odata.id attribute.  

![Store Full OData URL](Images/signed-form-store-full-odata-url.JPG)

![Parse base OData URL](Images/signed-form-store-base-odata-url.JPG)

### Download the Signature Image
The Pen Input result from the [Electronic Signatures Demo App](./ElectronicSignatures.md) was stored using the [File field type in CDS](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/file-attributes).  You could also use the [new Image field type](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/image-attributes) that supports full images too.

The connnector we need to use here is the [HTTP with Azure AD](https://docs.microsoft.com/en-us/connectors/webcontents/).  Add the action to your Flow and then click on the "..." and click "+ Add new connection".  You need to setup this with the CDS Azure AD Application Information.  Below is the configuration for Commercial O365

![Configure HTTP with Azure AD](Images/signed-form-HTTP-AAD-Config.JPG)

Now we need to configure the action itself.  Make a GET request to download the signed signature image using the base OData URL and the unique ID of the Signature entity as variables,

![HTTP with Azure AD Action Config](Images/signed-form-HTTP-AAD-action-setup.JPG)

### Format the JSON Response
The Word template action requires a specfiic format for image control types.  This action formats the download response properly.

![Format JSON](Images/signed-form-format-json.JPG)

### Populate the Word Template
Add a new action to Populate a Microsoft Word template.  Find the template file you created eariler and uploaded to OneDrive and configure this action.  Once you tell it the file you want to you use, you should now see each content control field available as inputs to the action step.  

![Word Template Action](Images/signed-form-word-template-action.JPG)


### Export the Word result as a PDF
Now we want to use the Convert Word Document to PDF action.  In order to use this, we first have to save the previous result to OneDrive to a temporary file location.  We can also delete the temporary file after we create the PDF file.

![Export to PDF Steps](Images/signed-form-export-PDF.JPG)

### Email the PDF
Finally we can email the copy of the generated PDF file.  Below is the setup for this,

![Email Step Setup](Images/signed-form-email-step.JPG)

## Final Result
Putting this all together, when we create a new Signature entity we now receive an email to with the attached and signed PDF form.

![Email Results](Images/signed-form-email-output.JPG)