# Google Doc to Data Table UE5 plugin 

# General information
UE5 Editor plugin that provides a convinient way for importing data from google spreadsheet into UE5 data table.

![Alt Text](Resources/demo.gif)

# How to install
* Clone the repository
* Unzip and copy GoogleDoc2DataTable folder into "your_ue5_project_folder/Plugins/". If Plugins folder does not exist in your project, just create it.
* Open your project in UE5
* Go to Edit -> Plugins -> Other. Enable GoogleDoc2DataTable

# Required Engine Modifications
* This version of plugin needs an engine modification to store google docs url per data table asset, so we won't have to enter URL each time editor is restarted, or working with more than one data table.
* Add `FString SourceURL` variable into UDataTable class header in engine source. Make it blueprint EditAnywhere.
* Add `SourceURL = SourceTable->SourceURL;` call into `UDataTable::CopyImportOptions` function to be able to copy SourceURL data while fetching data from google docs and recreating the data table.

# How to use

* Right click in a content browser, select: Blueprints -> Structure 
* Create a structure that matches data in your spreadsheet. Keep in mind that UE5 treats the first column as a lookup and handles it automatically so you don't need to create it in the Structure. More information on that here: https://docs.unrealengine.com/en-US/Gameplay/DataDriven/index.html
* Create a datatable ( right click in content browser: Miscellaneous -> DataTable ) and select structure you created in previous step
* Right click on the datatable. In the context menu you should see and option "Load from Google doc" ( 4th row from top ).
* A new window will appear. Enter your spreadsheet id into the input field. What is spreadsheet id ?

Let's say your google spreadsheet address is:
https://docs.google.com/spreadsheets/d/1YjC78QtDrHQzsyz7vNAWWetlKUNEgID3gjA1S0svFys/edit#gid=0

then spreadsheet id is this part: 1YjC78QtDrHQzsyz7vNAWWetlKUNEgID3gjA1S0svFys

* Important: Your spreadsheet needs to have public sharing turned on. Otherwise it will not work.

# Current limitations
* Works only with public spreadsheets ( link sharing has to be turned on ). Authorization was not implemented yet. 