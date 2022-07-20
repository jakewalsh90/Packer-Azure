# Packer
Packer deployment files for Azure

### How to use the files in this repo. 

1


2. Identify the image you wish to deploy using the Azure CLI. For example, the below finds all the Windows Desktop Offers, and then finds the Windows 11 SKUs - change this as required for your needs/locations:

    az vm image list-offers -l uksouth -p MicrosoftWindowsDesktop --query [].name -o tsv

    az vm image list-skus -l uksouth -f windows-11 -p MicrosoftWindowsDesktop --query [].name -o tsv

3. Create the required Resource Group for Packer:

    az group create -n Packer1 -l uksouth

4. Create a Service Principal for Packer to use:

    az ad sp create-for-rbac --query "{ client_id: appId, client_secret: password, tenant_id: tenant }"

This will output something similar to the below:

    { "client_id": “xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "client_secret": “xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "tenant_id": “xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" }

Within the packer file you wish to use, you will need to add this information to the file:

      "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "subscription_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",

5. We are now ready to run Packer. To run packer use the following command:

    ./ packer build demo.json

Packer will now run and create your image!