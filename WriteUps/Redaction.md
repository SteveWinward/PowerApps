# PII Redaction with Power Automate

# Sample Redaction Flow
Below is a link to download the sample solution Flow I demonstrate in the YouTube video.

https://github.com/SteveWinward/PowerApps/raw/master/WriteUps/Samples/Redaction/RedactionDemo_20210107140714.zip

Also, below is a link to a Word document that has content control types added which are used in the Flow sample.

https://github.com/SteveWinward/PowerApps/raw/master/WriteUps/Samples/Redaction/SurveyTemplate.docx

# Requirements
* An Azure subscription.
* A Power Automate Per User license (not the seeded O365 license).  You can get a 30 day free trial to use instead.

# Setup
* Create an Azure Text Analytics resource in your Azure subscription.
* Download the sample Word document and upload that to your OneDrive.
* Import the sample Flow.  
* The import will fail, but you can save a new Flow as a draft.  
* Update the Flow's Word for Business action to use the Word doc you previously updated
* Update the Text Analytics URL and the Text Analytics API Key to use your instance of the Text Analytics service.
* Save and text the Flow
