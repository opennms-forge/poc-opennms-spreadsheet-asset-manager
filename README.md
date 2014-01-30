## OpenNMS Spreadsheet Asset Manager ##

### Basic usage
The tool is provided as a executable Java-Archive (JAR). To run a executable JAR use the java command with the jar parameter like `java -jar`. It requires Java version 1.6 or higher. OpenNMS 1.10.x is supported, other version are not tested. If you run `java -jar OnmsSSAM.jar` to start the tool, it will response with a short how to use and what parameters it understands.
For every operation this tool needs a set of parameters to be able to talk to a remote OpenNMS by using the Rest-API.
This are the basic parameters that are always required:

* baseurl http://your_opennms_webapp/
* username TheUser
* password ThePassword

This tool uses the OpenDocumentFormat (ODF) for all spreadsheets. The spreadsheet format of ODF is called OpenDocumentSpreadsheet (ods). All generated files and file to use for updating a remote OpenNMS have to be in the ODS format.

### Read nodes and assets from a system
To read all nodes and there categories from a system, pass the basic parameters and the following two parameters:

* generateOds
* all-foreign-source

To read all nodes and assets from a defined Provisioning-Requisitions aka Foreign-Source, pass the basic parameters and the following two parameters:

* generateOds
* foreign-source NAME_OF_THE_FOREING-SOURCE

The result is going to be a spreadsheet per Provisioning-Requisitions named like the Provisioning-Requisitions in the temp folder of your system. The file with a complete path is going to be listed in the output of the tool.

The generated spreadsheets will just contain the used assets for the listed set of nodes. To have a more conclusive list, use a customized template file with all the assets needed already listed in the first row. The template feature also offers the ability to customize the layout of generated spreadsheets. To use the template feature use this additional option:

* OdsTemplate THE_ODS_TEMPLATE_FILE

### Write assets for nodes into a system

* ods-file-source THE_ODS_SPEADSHEET_FILE
* foreign-source NAME_OF_THE_FOREING-SOURCE

Using this options is going to push the changes into the named Provisioning-Requisition aka Foreign-Source. The changes are not applied yet, the Provisioning-Requisition is in pending state. Until it is synchronized the changes will not appear on the nodes.
To change the assets of nodes and synchronize the changes directly use this additional option:

* synchronize

Please be careful with this tool, backup your Provisioning-Requisitions before playing around with this tool.

### How to get it
The following steps are required to build this tool from source. A properly installed Java system and Maven is required.

mkdir SRC_OpenNMS_Tools_Sample
cd SRC_OpenNMS_Tools_Sample

git clone https://git.gitorious.org/opennms-rest-client-api/opennms-rest-client-api.git
cd opennms-rest-client-api
mvn clean install -DskipTests
cd ..

git clone https://git.gitorious.org/opennms-rest-provisioning/opennms-rest-provisioning.git
cd opennms-rest-provisioning
mvn clean install -DskipTests
cd ..

git clone https://git.gitorious.org/opennms-spreadsheet-asset-manager/opennms-spreadsheet-asset-manager.git
cd opennms-spreadsheet-asset-manager
mvn clean install assembly:single -DskipTests
cp target/opennms-spreadsheet-asset-manager-1.0-SNAPSHOT-jar-with-dependencies.jar OnmsSSAM.jar

Now the tools is ready to use as described in this article as `OnmsSSAM.jar`.  

**Thanks for computing with OpenNMS**
