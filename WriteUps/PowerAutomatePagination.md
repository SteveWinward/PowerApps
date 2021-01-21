# Pagination with Power Automate
I published a YouTube video on how to use vairous pagination strategies with Power Automate.  The link is below,

https://youtu.be/5NtzcfmSGes

# Sample Pagination Solution
Below is a link to download the sample solution file I demonstrate in the YouTube video.

https://github.com/SteveWinward/PowerApps/raw/master/WriteUps/Samples/PowerAutomatePagination/PaginatedDemoSolution_1_0_0_2_managed.zip

Also, below is a link to an CSV file to populate the DemoPagingEntity custom table in the Dataverse.

https://github.com/SteveWinward/PowerApps/raw/master/WriteUps/Samples/PowerAutomatePagination/SamplePagingData.csv

# Install Steps
1. Make sure you have an O365 tenant to use.  You can create a trial O365 tenant see notes below,

    https://danusher.com/how-do-i-cloud/how-to-create-an-e3-e5-trial-tenant/

2. Make sure you have a Power Platform Environment to deploy the solution to.  How to create a trial Environment here,

    https://docs.microsoft.com/en-us/power-platform/admin/trial-environments#multiple-ways-to-start-a-trial

3. Import the PaginatedDemoSolution solution file (see download link above).

4. Go to the Solution and to the sample table entity.
  * Choose get data from Excel
  * Choose the SamplePagingData.csv file (see download link above) referenced above to populate the sample data
