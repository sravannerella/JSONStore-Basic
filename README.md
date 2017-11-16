# JSONStore-Basic

## Create and Usage of IBM JSONStore using MobileFirstPlatform 7.1 CLI

1) Creation of Project can be done with the following command in your terminal/command prompt
	- `mfp create jsonStoreProject`
	- Now change your directory to the jsonStoreProject and then navigate to apps folder using `cd jsonStoreProject/apps`

2) Now let's create hybrid app with following command and then add jsonstore to the app
	- `mfp add hybrid jsonApp`
	- Navigate inside the jsonApp directory using `cd jsonApp`
	- Execute following command to add jsonstore to the app. `mfp add feature jsonstore`

3) Now set the your mobile environment with the following command:
	- ANdroid: `mfp add environment android`
	- iPhone: `mfp add environment iphone`

4) Open the jsonApp folder in your favorite editor
5) As you can see, this folder has your device enviroment folder, common, and legal folder. Let's navigate to the `common/js/main.js` file.

6) Follow the comments, understand the code and then Paste the following code in your `main.js` file .
		
		`function wlCommonInit(){

			// Collection Name
			var collectionName = 'data';

			// Collection Data Attributes and search Feilds
			var collections = {
				data : {
					searchFields : {name: 'string', age: 'integer'}
				}
			}

			// Collection Login Options 
			/*
			 * Username: jsonstore (default)
			 * Password: 
			 * 
			 * clear: false - OPtion to delete the data
			 */
			var options = {
				username: 'Sravan',
				password: 'Nerella',
				clear: false
			}

			// Connecting to JSONStore
			WL.JSONStore.init(collections, options)

			// After connecting to the JSONStore, Add data to the 
			// collection
			.then(function(){
				return WL.JSONStore.get(collectionName).add({
					name: 'Sravan',
					age: 22
				});
			})

			// After adding data to the collection, log how many 
			// documents are added and display to the console
			.then(function(numberOfDocumentsAdded){
				console.log("Added: " + numberOfDocumentsAdded);
				return WL.JSONStore.get(collectionName).findAll();
			})

			// Display the results after returning from previous step
			.then(function(findResults){
				console.log("Results: " + 
					JSON.stringify(findResults, null, ' '));
			})

			// If anything went wrong, Fail function gets triggered
			.fail(function(err){
				console.log("Failed: "+ err.toString());
			})

		}`

7) Open your terminal/Command Prompt and build the project using:
	- `mfp build` and then `mfp deploy` (deprecated)
	- `mfp push` (Working)

8) Once the app is complete deploying to the run time. Open the Mobile First Platform console with the following command:
	- `mfp console`
	
9) Find jsonApp in your Applications section. In the enviroment click on the Common resources (folder icon).
10) Click on Preview version. This should open your app with `Hello MobileFirst`. 
11) Open your web inspector, which will show the data you inserted being added.
