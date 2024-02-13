REQUIREMENTS:

NodeJs (v12.16.3)
Yarn (1.22.17 - latest at the time) : npm install --global yarn


STEPS TO BUILD AND RUN UI LOCALLY:

1. Clone the repo : git clone  https://github.com/onap/ccsdk-features
2. Change the authentication from oauth to basic in
	~/ccsdk-features/sdnr/wt/odlux/framework/src/index.dev.html
3. Change proxy targets in /home/vikas/code/ccsdk-features/sdnr/wt/odlux/framework/webpack.config.js from "http://sdnr:8181" to the ip address of the server where the api gateway is running. 
	This will be used by the UI to get the data from rest endpoints e.g. target: "http://54.242.17.220:30181".
4. Now we need to build the base app which will wrap all the other apps like connect, faultApp etc.

	Go to ccsdk-features/sdnr/wt/odlux/framework and run the below commands :
-->	yarn
-->	yarn run vendor:dev
-->	yarn run build:dev

1. After this there will be a dist folder created at ccsdk-features/sdnr/wt/odlux. 
	Now we can build the apps we want by going to the respective location and running yarn build:dev. 
	e.g go to ccsdk-features/sdnr/wt/odlux/apps/connect and run yarn build:dev. 
	For the UI to come up we need at least “connect“ and “faultApp“. 
	This can be changed in /home/vikas/code/ccsdk-features/sdnr/wt/odlux/framework/src/index.dev.html
2. Once we build the required apps we can run the gui by below command.
-->	cd ccsdk-features/sdnr/wt/odlux/framework
-->	yarn start
-->	GUI can be accessed from localhost:3100



CHANGING THE ONAP LOGO IN GUI:


-->	cd features/sdnr/wt/odlux/installer
-->	mvn clean install
-->	cd features/sdnr/wt/odlux/installer/target/stage 
--> 	unzip <filename.zip>
-->	cd features/sdnr/wt/odlux/installer/target/stage/odlux/images/
		Here we need to change the onaplogo to wisigLogo in onapLogo.gif image.
		
-->	cd features/sdnr/wt/odlux/installer/target/stage
-->	zip -r <filename>.zip help odlux
-->	cd sdnc-oam/installation/sdnc-web
-->	vi pom.xml
			In pom.xml we can add these elements in dependency element in our project. which are refering the sdk features.
			Elements like groupId, artifactId, version,type, classifier, scope and systempath.
			ex:- 	<groupId>org.onap.ccsdk.features.sdnr.wt</groupId>
					<artifactId>sdnr-wt-odlux-installer</artifactId>
					<version>1.7.0</version>
					<type>zip</type>
					<classifier>repo</classifier>
					<scope>system</scope>
					<systemPath>---/path/of/the/zip/filename---</systemPath>
			
			In image element we need to change the image name.
			
-->	cd sdnc-oam/installation/sdnc-web
-->	mvn clean install
-->	cd sdnc-oam/csit/scripts/sdnr/docker-compose/
-->	vi docker-compose-single-sdnr-web.override.yaml
			In this file we need to modify the sdnc-we image name and tag. what we are mention before in pom.xml.
			
-->	./start_sdnr.sh

		GUI can be accessed from localhost:8282




		


FYI:

List of versions of nodejs
-->	nvm list

change the version
-->	nvm use <v16.20.2>

 version of Node.js
 -->	nvm version
 
 
https://github.com/onap/sdnc-oam/tree/london
https://github.com/onap/ccsdk-features/tree/london