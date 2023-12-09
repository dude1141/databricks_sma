# databricks_sma
databricks_practice
points to remember

cluster pools resources for you cluster
pools of resources for you using lcuster pools


job clusters are not created manually,

ADLS azure data lake storage

session scope authentication
cluster scope authentication
Azure active directory---looks at roles user has been assigned to ADLS using IAM
Unity catalog--admin can assign permission to users---premium

0:50

ADLS comes with two 2 keys

access keys--- spark.conf.set("fs.azure,account.key...windows.net","adsfsdafs")
reference data from ADLs---from databricks we need driver called abfs(Azure blob file system)

abfs[s]:// container @storage_account/folderpath/file_name

abfs[s]://file_system@account_name.dfs.core.windows.net/<path>/<path>/<file_name>

SAS --shared access signature Token
1) fined grained access storage

2) restrict access to specific resource

3) allow specific permisions

4) restruc access to time period

5)  limit accesss to IP address



accessing using SAS token

spark.conf.set("fs.azure.account.auth.type.<storage-account>.dfs.core.windows.net", "SAS")

spark.conf.set("fs.azure.sas.token.provider.type.<storage-account>.dfs.core.windows.net", "org.apache.hadoop.fs.azurebfs.sas.FixedSASTokenProvider")

spark.conf.set("fs.azure.sas.fixed.token.<storage-account>.dfs.core.windows.net", dbutils.secrets.get(scope="<scope>", key="<sas-token-key>"))



service_prinicipal --better security and traceability
Azure AD application---

access control(IAM)
we have given storage blob data contributor access on our storage account formualdl1 to the service principal

cluster scoped ---we set the secret and spark conf set on the cluster side instead of databricks notebook.



in certain scenarios , we have to controls users or specific users
we use Azure active directory --using RBAC only on premium tier




dbsecrets.utilty

it really avoids exposed secrets to public, without comprising your secrets


creation of clientid,tentatid and clientsecret and use later for mounting etc...and set them in spark conf.set

to create secret scope , you need azure vault where you get valult URI and reosurceid and later they are used to list and get secrets from azure

formual_dl_account_key=dbutils.secrets.get(scope='formualdl1', key='formualdl1-account-key') 


DBFS or Databricks File System

here, is a distributed file system mounted on the Data bricks workspace.
can be accessed from databricks ,an abstraction layer on top of azure blob storage

DBFS root is where display results are stored or query results , managed tables default creation is dbfs root

