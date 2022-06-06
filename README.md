# BHL GBIF test


## Dataset

e6532554-1406-45ee-a574-9b3947c7ffbe

## Step 1 Create dataset on GBIF

Create a dataset on GBIF using registry API. The **publishingOrganizationKey** is the publisher UUID that you see in the link to the publisher page: http://www.gbif.org/publisher/92f51af1-e917-49bc-a8ed-014ed3a77bec. You also need a **installationKey** provided by GBIF, and you also need to authenticate the call using your GBIF portal username and password.

http://api.gbif.org/v1/dataset

POST

```javascript
{
	"publishingOrganizationKey":"92f51af1-e917-49bc-a8ed-014ed3a77bec",
	"installationKey":"**<your key here>**",
	"title":"BHL test",
	"type":"CHECKLIST" 
}
```
RESPONSE

```javascript
“e6532554-1406-45ee-a574-9b3947c7ffbe”
```

We now have a UUID (e6532554-1406-45ee-a574-9b3947c7ffb) for the dataset, which lives here: https://www.gbif.org/dataset/e6532554-1406-45ee-a574-9b3947c7ffb


## Step 2 Create and validate Darwin Core archive

Now we need to create the Darwin Core archive. 
I then generated a meta.xml file, and finally the Darwin Core Archive (DwC-A) (which is simply a zip file):

```
zip dwca.zip eml.xml meta.xml data.tsv
```

Next we need to check that the DwC-A file is valid using the [Darwin Core Archive Validator](https://www.gbif.org/tools/data-validator).

## Step 3 Create endpoint

Now we need to tell GBIF where to get the data. In this example, the Darwin Core Archive file is hosted by Github (make sure you link to the raw file).

http://api.gbif.org/v1/dataset/e6532554-1406-45ee-a574-9b3947c7ffbe/endpoint

POST
```javascript
{
  “type”:”DWC_ARCHIVE”,
  “url”:”https://dl.dropboxusercontent.com/u/639486/dwca.zip”
}
```

RESPONSE 

HTTP 201 Created

```javascript
99444
```

## Step 4

Wait for GBIF to index the data…




