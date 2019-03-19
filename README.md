# HAPI FHIR & SQL DB with SmartHospital
Repository to help set up HAPI FHIR hosted on Azure for Smart Hospital system and Azure SQL database.


FHIR Server Setup
Hosting Web service on azure:
Go to (https://github.com/hansenms/fhir-azure/tree/master/hapi-fhir-sql) and follow the instructions provided on the page. This provides a template that deploys the infrastructure for running the HAPI FHIR example server as a Azure Web App with an Azure SQL Database backend. The Web App will be configured with all necessary connection strings, java versions, etc. Click the ‘Deploy to Azure’ button at the bottom of the page.
A .war file will need to be generated for deployment. To do this follow the instructions on (https://github.com/hansenms/fhir-azure/tree/master/hapi-fhir-sql). Then copy the hapi-fhir-jpaserver-example.war (from the target folder) file to the D:\home\site\wwwroot\webapps folder of the Azure Web App (using the Kudu console).
After deployment visit the web app (e.g. (https://WEBSITENAME.azurewebsites.net/hapi-fhir-jpaserver-example/)) with a browser to make sure it is up and running.
Uploading mock data
The next step is to generate sample data on the FHIR server hosted on Azure. To do this follow the instructions from (https://github.com/smart-on-fhir/sample-patients-stu3). You will need to run a command like this using python 2:

python2 generate.py --write-fhir ../out --id-prefix "nhs"

This adds a nhs prefix before ids.
 
Then you can upload this generated data on the azure hosted fhir server by following the instructions given in (https://github.com/smart-on-fhir/tag-uploader). Do npm install after cloning the repository.

From the previous step, we have the sample data loaded in the out folder. This can be moved to the directory under tag-uploader. We can rename the javascript file index.js to tag-uploader.js. Then run the following statements. Replace “nhs” with any tag. In the second command replace the url given with the fhir server url (baseDstu3)

node tag-uploader -d out -t "nhs" -w
node tag-uploader -d out -t "nhs" -S (http://smarthospitalhapifhir.azurewebsites.net/hapi-fhir-jpaserver-example/baseDstu3)

