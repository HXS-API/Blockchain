# Trial Blockchain User Interface

We're building a simplied interface to test a humanitarian blockchain use case in partnership with [OneRelief](https://onereliefapp.com).

## User Interface

![User Interface](https://github.com/HXS-API/Blockchain/blob/master/Images/blockchain_ui_900.png)

### Login Header

Instead of logging into the interface using an email and password, the interface will utilize **Node Id** and **Node User** inputs. These inputs will enable the trial to differentiate between participating organizations and between individuals working at the organizations.

* **Node ID**s will be used for the names of organizations participating in the trial, for example **Oxfam** or **SaveTheChildren**
* **Node Users** will be for individuals, for example **JohnDoe**. 

### Menu

The main menue will give node users with the ability to:
* **View** or refresh raw JSON data in the ledger view window
* **Parse** the data an turn it into a human readable form, matching the way data is presented by IATI's Preview tool (example: [Oxfam GB]() aid activity files, for activities in Afghanistan)
* **Enter** new or edit existing block data
* **Publish** new or updated data

### Ledger

The ledger window displays blocks of raw JSON formatted data which the node user is authorized to view and edit.

The user interface will populate the window via pulling and displaying block data after the user logs into the interface. The data can be parsed and viewed in human readable form matching how IATI's Preview tool displays data. The data can be **Refreshed** at any time.

**JSON**

image

**IATI**

image

### Data Input Forms

Selecting **Enter or Edit Block Data** from the main menu will replace the data view window with a series of data input forms corresponding with IATI information fields which the trial has decided to use.

Interface users can use any of the fields to enter data. Expect for **IATI-identifier**, all the fields are optional. Entering an existing IATI-identifier will auto populate the forms, enabling a user to edit existing data.

# Development

To a large degree, the user interface will simulate a blockchain network. Users will immutable data blocks, which will be added to the top of a ledger (an expanding JSON file). Users will employ a parser to turn the data into information and forms to add new blocks.

### Pages as Nodes

The interface will utilize website pages as separate blockchain nodes. Utilizing a node template, page nodes will be added to the UI website for each individual trial participant.

### Node Ledgers

Each node will only populate with data which the individual user is authorized to edit. The ledger will populate with raw JSON data.

### Invisible Data and Sharing Rules

To simplify construction of the UI, data pertaining to Node ID and Node User will be collected and added to blocks, but the data will not be displayed (unless they have authored the data or they are listed as authorized by another user). The data will enable each Node to identify and display only data which individual users are authorized to edit.

Authorize Node ID and Node User data input forms will be included in the Enter Data list, to collect this information. Multiple IDs or Users can be added to the forms separated by commas. Entering "Public" into either of the form spaces or leaving the spaces empty will make data from all the forms public.

Each form will include **Node ID** and **Node User** fields, enabling participants to experiment with controlling information access.


### Data Parsing

The **Parse** feature will display data generally in the same way as IATI's Preview tool. It will:

* Aggrigate block data by **IATI-identifier**, displaying only the latest viersion of block data (add a plus or minus to open data fields) and use the idenfier as a heading).
* Only display information headings and information which has been published and not from empty fields
* Only display information which a Node User is authorized to view
* Display non-IATI fields like Node ID and Node User under the IATI identifier, if included in the data
* Display data in reverse chronological order
* Add buttons to view only data shared by Node ID or Node User (org sepecific or user specific)
* Color Red and add field duplicates which conflict and have been added by another user
* Add button to enable a user to flag red their own conflicts (over a history of blocks, to show updates)


### Consensus

Interested in using the Parser feature to flag data inputs which don't match. The idea will be enable individuals to see data dinscrepancies (updates made by others) to force different users to come to consensus by adopting a version. Adopting a version will enter an identical block authored by the individual.

The Parser will only display IATI-identifiers and subsequant data which match (publidhed by only one individual or by two or more which are the same). In the case of unmathing data, if it is authored by the same person it will be deemed "updated". Filters described above, enable unmatching identifiers (by different authors) to be displayed.

In all cases the oldest version won't be red.



### Entering and Publishing New Blocks

The trial UI will list basic forms (and perhaps add a full IATI vversion). The forms will include Node ID and Node User sub-fields.

Generate a JSON array, including a **codelist** field (nested or separate) for IDs and Uers.


### Hashing

Each block will be hashed. Only data (not old hash and timestamp) will be included in the hashed set. 

Hashes will principally used to establish consensus within an organization and establish a consensus version for sharing outside of an organization.

(orgs and individuals listed in private can see red conflict flags)(?)

### Data Storage

To keep the trial UI simple, it will utilize a stored JSON file as a storage ledger.
