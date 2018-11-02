# mongodb-nodejs

commands :

	reffrence : https://www.youtube.com/watch?v=Do_Hsb_Hs3c

type this commands from project directory
-----------------------------------------

->npm install --save express

->npm install -g express-generator

if it not work then try with sudo for admin permiision 

->npm install jade

->express [project name -it will create folder with this name and adding all related files on it] like : express sampsite


then open newly created folder and open package.json

and add dependancys:

"kerberos":"~0.0.7",
"mongodb":"~2.0.33"

and save file 

open terminal again and go to sampsite directory

then 

run command 
->npm install
->mkdir data 
->npm start

and keep this terminal as it is


now open browser and type in url localhost:3000 it shows express (welcome to express)


now open new terminal and on root directory where mongodb install so, type command
->mongodb --dbpath /opt/lamp/htdocs/mongodb_node/smpsite/data/

ok so, now open another third terminal and on root directory type command :
-> mongo (to start mongo db)

ok now create new database or switch to alredy exist database 
type command :

-> use sampsite

now you are on sampsite database now check students collections are there or not :
-> show collections

collections means kind tables in mysql word.

if you want to create new collection then type :

->db.createCollection('students');

so, now add some data into students collection and that called document type command:

->db.customers.insert([{"student":"Mukund","street":"207 raj appartment","city":"Ahmedabad","state":"Gujarat","sex":"M","gpa":3.5}]);


you can check this inserted records by this command

->db.customers.find().pretty() 
it will all the records from customers collections


ok now it's done


now open app.js file from sampsite folder and add few line of code for mongodb connection

var mongo = require('mongodb');

and other then this keep as it is on this file.

now open index.js file from routes folder and add few line of code 

var mongodb = require('mongodb');


And this new routes


//start custom new route cteated 

router.get('/thelist', function(req, res) {
	var MongoClient = mongodb.MongoClient;
	var url = "mongodb://localhost:27017/sampsite";
	// here 27017 is defaullt mongodb port 
	// here sampsite is my database name to connect with node

	//now make connection 

	MongoClient.connect(url,function(err,db)){
		if(err){
	             console.log('unable to connect the server.',err);		
		}else{
	             console.log('you are connected to database');
	             var collections = db.collection('students');
		     collections.find({}).toArray(function(err,result){
		       if(err){
                           res.send(err);
		       }else if(result.length){
		           res.render('studentlist',{
				"studentlist":result	
		           });  		
		       }else{
		           res.send("No Records Found");	
		       }

		       db.close();
                     });						
		}
	});	
		
});

//End custom new route created 



Now create studentlist.jade file on views directory


 






