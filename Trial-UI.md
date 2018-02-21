# User Interface 1.0

The simplified **web interface** below will give humanitarian organizations and donors an opportunity to test and evaluate first hand how a simulated **IATI compliant blockchain network** can work and be used to carry out basic information sharing exchanges.

![User Interface](https://github.com/HXS-API/Blockchain/blob/master/Images/UI10.png)

# UI Elements

### Login Header

![Header](https://github.com/HXS-API/Blockchain/blob/master/Images/login_900.png)

To use the interface to log into a network node, staff from humanitarian and donor organizations must enter the following:

* **Node ID** - The name of their organization, for example **Oxfam** or **SaveTheChildren**
* **Node User** - Their name or a short or anonymized version, for example **JohnDoe** or **JDoe**.

### Menu

![Menu](https://github.com/HXS-API/Blockchain/blob/master/Images/Menu_900.png)

The interface’s **main menu** provides logged in users with the ability to:

* **Refresh** the ledger window to import and view any new data changes
* **Parse** and format ledger data in the window to look similar to data formatted by [IATI's Data Previewer](http://preview.iatistandard.org/index.php?url=http%3A//iati.oxfam.org.uk/xml/oxfamgb-af.xml)
* **Enter** or update ledger data by using a form to create a new data block to publish
* **Publish** a new data block created to add to the ledger

### Ledger Window

![JSON](https://github.com/HXS-API/Blockchain/blob/master/Images/jsondata.png)

After a node user logs in, the interface will retrieve raw JSON data from the blockchain's centralized ledger and display the data in the ledger window.

The interface will **only** retrieve and display blocks of data which the logged in user has **published** (authored) or which other node users have given the user **permission** to view and update.

**Parsed View**

Data displayed in the window can be **parsed** and reformatted to look similar to data formatted by IATI's Data Previewer. To accomplish this, the parser will aggregate block data by **IATI-identifier** and display only the most up-to-date information entered in IATI information fields creating a list of composite IATI activity files.

Node users will be able to expand or open listings to display their contents or close them.

![IATI](https://github.com/HXS-API/Blockchain/blob/master/Images/parsed_fields.png)

### Entering and Updating Data

Node users can replace the window with a **form** to enter a new or updated block of JSON data to the centralized ledger.

![Forms](https://github.com/HXS-API/Blockchain/blob/master/Images/forms_900.png)

The form uses IATI information fields as inputs. Adding an existing IATI identifier will auto-populate the form, making it easy to replicate an existing data block and update specific information fields.

To control information access, node users can give other users and organizations permission to view and update information on a field-by-field basis or leave the permissions empty to make the information public.

### Conflicts

![Conflicting Data](https://github.com/HXS-API/Blockchain/blob/master/Images/conflict_a900.png)

The parser aggregates block data by IATI-identifier and only displays the most current data found in IATI information fields based on block date/time stamps. As long as conflicting information is published by the same author, these conflicts are treated as updates.

If however different information, referencing the same IATI-identifier, is published by different authors, the parser will display all of the versions and color the newer conflicting version red and add the author’s Node ID and Node User identifier. The parser will treat the older version as the most up-to-date until a newer block is published by either author matching the other’s or an author publishes a block referencing the IATI-identifier with no information in the conflicting field.

### Consensus

Through controlling informational access using **permissions** and **flagging conflicts**, the user interface makes it easy for individuals, teams and peer groups to securely start and develop IATI activity files and reach consensus on information to update and make public. This includes checking information traversability and correcting pathway issues cross-connecting activity files, for example pathways properly documenting partnerships, related activities and funding transactions.

### Data Storage

User Interface version 1.0 will store data in a single central JSON file. The file will serve as a blockchain ledger and it will grow in increments as blocks of data are **published** and added to the ledger by different node users.

Each data block will have the following attributes:

* **Block Number** - Block's numbered position in the blockchain
* **Previous Hash** - Hash of the previous block
* **ISO Datetime** - ISO data and time that the current block was published
* **Author Node ID** - Node ID of the author who published the block
* **Author Node User** - Node User identifier of the author who published the block
* **Data** - Information published by organizations, reported using IATI information fields
* **Data Hash** - Hash of just the data
* **Current Hash** - Hash of the current block

**Example Data Block**

```
{
   "block-number": "101",
   "previous-hash": "E9843B564E1E636CB45C3B44ED71FDBF6C94B7891DC10836194D1F34D09BCE48",
   "iso-datetime": "2018-01-01T01:01:01+00:00",
   "author-nodeid": "oxfamgb",
   "author-nodeuser": "johndoe",
   "data": {
      "iati-identifier": "AA-AAA-123456789-ABC123",
      "iati-identifier-permission": {
         "iati-identifier-permission-nodeid": [
            "oxfamgb",
            "savethechildren"
         ],
         "iati-identifier-permission-nodeuser": [
            "johndoe",
            "janedoe"
         ]
      },
      "reporting-org": "Organization A",
      "reporting-org-permission": {
         "reporting-org-permission-nodeid": [
            "oxfamgb",
            "savethechildren"
         ],
         "reporting-org-permission-nodeuser": [
            "johndoe",
            "janedoe"
         ]
      }
   },
   "data-hash":"38C165F02BE2FB2768161424A868838B209E2900B960C2EFB15258FAB576E634",
   "current-hash": "1B502C79034DBD286AB3A9B221EE58E6EFEE993D03C64BCF7713D486F6803974"
}
```

### IATI Data Storage

The **Data** attribute is designed to store information provided by organizations and donors. **IATI information fields** are used as sub-attributes. 

Sub-attributes are paired with **permission** attributes , providing node users with the ability to control informational access on a field-by-field basis. Permission controls will enable node users to share information internally, with specific peers or peer organizations as well as test reporting workflows and information release strategies.

Users can enter multiple Node IDs or Node Users to the fields separated by commas or leave the fields empty, making information in the IATI fields public. Organizations and donors can also use as many or as few IATI information fields as they like or add information incrementally via a series of block updates. 

Because IATI activity files are referenced by their unique activity identifier, node users must enter a new or existing identifier into the **IATI-identifier** field to publish a block of data to the central ledger.

### Hash Generation

The interface will experiment with hashing **IATI data** as well as the **whole** current data block, using the SHA-256 hash function. Generating a separate hash for IATI data will give node users the ability to check and unify block update versions before making information public for example.
 
# Testing

The user interface is being built to test how an IATI compliant blockchain application can potenitially function and be used to facilitate information sharing between humanitarian organizations and between humanitarian organizations and donors, including humanitarian crowdfunding platforms.

Organizations and donors participating in testing the interface will be asked to experiment with using the interface to:

* Organizations: Start one or more activity files
* Organizations: Edit or update a file jointly with one or more other node users
* Organizations: Selectively share file information with other organizations or with prospective donors via their nodes
* Organizations: Publish an activity file or a portion of a file to the public with no permission restrictions
* Organizations/Donors: Use the parser to learn about and track activities
* Donors: Start an activity file signalling a partnership with an aid organization
* Organization: Publish more specific information about an aid activity
* Donor: Document a planned disbursement
* Donor: Create a funding condition to test
* Donor: Document a transaction disbursing funds to an organization
* Organization: Document the recipe of a transaction from a donor
* Organization: Update a file to report the results of an aid activity
* Donor: Update a file to report the results of a funding activity
* Organization: Reporting a related activity
