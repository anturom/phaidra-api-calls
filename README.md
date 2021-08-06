# Phaidra Sandbox API Calls

These are the steps I followed in order to create a PHAIDRA container that has two members (a PDF attachment and an image). 

> Before you run the curl commands below:
>
>    - Change the terminal's current directory to the one where this project was cloned. All file paths are relative to this directory.
>    - Replace `username:password` with your actual PHAIDRA credentials.

## Step 1: Create empty container

```
curl -X POST -u username:password "https://services.phaidra-sandbox.univie.ac.at/api/container/create" -F "metadata=@container_metadata.json"
```

## Step 2: Create PDF

```
curl -X POST -u username:password "https://services.phaidra-sandbox.univie.ac.at/api/document/create" -F "metadata=@pdf_metadata.json" -F "file=@loremipsum.pdf" -F "mimetype=application/pdf"
```

## Step 3: Add PDF to container

Here, `o:1` is the identifier of the parent container and `o:2` is identifier of the PDF member, both returned in the response of the respective previous calls. Make sure to replace these with the actual identifiers.

```
curl -X POST -u username:password "https://services.phaidra-sandbox.univie.ac.at/api/object/o:1/relationship/add" -F "predicate=http://pcdm.org/models#hasMember" -F "object=info:fedora/o:2"
```

## Step 4: Create image

```
curl -X POST -u username:password -F "file=@shapes.jpg" -F metadata=@image_metadata.json https://services.phaidra-sandbox.univie.ac.at/api/picture/create
```

## Step 5: Add image to container

Again, `o:1` is the identifier of the parent container and `o:2` is identifier of the image, both returned in the response of the respective previous calls. Make sure to replace these with the actual identifiers.

```
curl -X POST -u username:password "https://services.phaidra-sandbox.univie.ac.at/api/object/o:1/relationship/add" -F "predicate=http://pcdm.org/models#hasMember" -F "object=info:fedora/o:2"
```