## Update war files
Updating the war files is the same for all versions:
- Undeploy applications with the tomcat manager.
- Place the .war files in the webapp directory

The context of the viewer-admin.war is changed, make sure this is done when deploying a update. To check this go to: 
`<tomcat-dir>/conf/Catalina/localhost/viewer-admin.xml`

There, check the <Context> tag:
`<Context path="/viewer-admin" crossContext="true" antiJARLocking="true" disableURLRewriting="true">`

check if the tag has a **'crossContext="true"'** attribute.

## Update Database
Good news and bad news... \\
The Bad: You have to update the database by executing a script on the database...
The Good: After updating to 4.3 you don't have to execute scripts on the database any more when updating to later version (4.3+). We implemented a auto database synchronizer that updates the database schema to the correct version.

### Update from 4.2 to 4.3
Updating the database to the new version can be done with the following script:

[Postgres update 4.2 > 4.3](http://github.com/flamingo-geocms/flamingo/releases/download/v4.3/pg_update_4.2_to_4.3.sql)

[Oracle update 4.2 > 4.3](http://github.com/flamingo-geocms/flamingo/releases/download/v4.3/ora_update_4.2_to_4.3.sql)


### Update from 4.2.1 to 4.3
This update is a bit harder, because it's a unofficial update... You first have to determine the current version of the database schema and then execute the correct scripts.
The best way to do this is:
* get the update script 4.2 > 4.3.
* Open the script and check the sub update scripts (scripts are seperated with '-- script xx').
* Open a database client to check if a sub update script is already executed on the database. Do this by checking if there is a:
  1. column 'value' in table 'layer_details, If so, skip sub script 14 and execute the rest of the script
  2. table 'geo_service_style_libraries', if so also skip sub script 15 and execute the rest of the script
  3. column 'extra_legend_parameters' in the table 'style_library', if so also skip sub script 16 and execute the rest of the script
  4. column 'value' in the table 'application_layer_details', if so also skip sub script 17 and execute the rest of the script
  5. table 'feature_type_relation', if so also skip sub script 18 and execute the rest of the script
  6. column 'feature_type' in the table 'configured_attribute', if so also skip sub script 19 and execute the rest of the script
  7. table 'metadata', if so also skip sub script 20 and execute the rest of the script



