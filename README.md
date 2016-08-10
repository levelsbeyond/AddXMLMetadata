# Add XML Metadata to Assets

This set of workflows is to take a user selected file of xml formatted metadata and add it to existing assets in Reach Engine. It removes the "Needs Metadata" category off of the assets it adds to.

## Import Order
1. xmlToJsonSubflow.xml
2. addXMLMetadataToAssetSubflow.xml
3. addXMLMetadataToAssets.xml

## Requirements
1. Must have the following metadata fields in Reach Engine:
|Name|Label|Type|XML Name|
|----|-----|----|--------|
|videoID|videoID|Text(small)|uuid|
|shootDate|shootDate|Date|date|
|eventType|eventType|Text(small)|event|
|cameraCard|cameraCard|Text(small)|cardNumber|
|camera|camera|Text(small)|camera|
|shooter|shooter|Text(small)|shooter|

2. Included is a sample XML file that shows the format that every XML file should have.
3. The file names in the XML file need to match up with assets that are in Reach Engine already.

## Testing
Import the workflows into Reach Engine. Create the needed metadata fields if not already present. Create the XML to import. The names used in the XML file must be the names of assets already ingested into Reach Engine. Run the workflow and confirm that the metadata properly assigns to each asset that was in the XML file.

## Descriptions
### addXMLMetadataToAssets
Takes the file that the user selects as input. It separates each "file" object out of the xml and creates a subflow for each one it finds.
### addXMLMetadataToAssetSubflow
Kicks off a subflow with the XML information that returns the metadata in JSON format. It then takes the filename and queries to find that asset in Reach Engine (this works for both Timelines and other assets). The workflow fails if the asset is not in Reach Engine. After getting the asset, it assigns the JSON metadata to it and removes the "Needs Metadata" category.
### xmlToJsonSubflow
Recieves an XML object and removes the six configured fields from it. Those fields get written into a JSON object and returned to the parent workflow.
