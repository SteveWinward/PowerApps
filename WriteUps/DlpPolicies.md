# Enable DLP Policies with HTTP Connectors
The documentation for DLP policies can be found below,

https://docs.microsoft.com/en-us/power-platform/admin/prevent-data-loss

If you want to include HTTP connectors to a DLP policy, you need to update the schema version for the DLP policy.  Today, you can only do that via PowerShell.  Below is a sample script to do that,

````
# Commerical Endpoint
Add-PowerAppsAccount

# GCC Endpoint
# Add-PowerAppsAccount -Endpoint usgov

# GCC High Endpoint
Add-PowerAppsAccount -Endpoint usgovhigh

# Get the list of DLP Policies to find the GUID you need
Get-AdminDlpPolicy

# Set the specific DLP Policy (by GUID) to update to the new schema
Set-AdminDlpPolicy -SchemaVersion '2018-11-01' -PolicyName '<INPUT_DLP_GUID_HERE>'

````

After you run the script, refresh your DLP policy through the browser and you should now see the HTTP connectors at the very bottom of the list in the "No business data allowed" section.
