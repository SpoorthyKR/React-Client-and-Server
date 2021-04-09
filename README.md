# React-Client-and-Server

In this program. I have created a React App with Node Backend.
Step 1 : Create Reactnodeapp blank folder and drag that to Visual studio code. to create this project we need to run the program in new terminal npm init -y, This will
create the package.json file. which will allow to keep track of all folders
step 2: We need to create a new server folder in reactnodeapp. and then add new js file called index.js We'll use Express 
to create a simple web server for us which runs on port 3001 if no value is given for the environment variable PORT (Heroku will set this value when we deploy our app).
step 3: Then in terminal we will install express as dependencies to use it. npm i express After that, we will create a script in package.json that will start our web server when we run it with npm start
Finally, we can run our app using this script by running npm start in our terminal and we should see that it is running on port 3001

Step 4: Create an API Endpoint
We want to use our Node and Express server as an API, so that it can give our React app data, change that data, or do some other operation only a server can do.
In our case, we will simply send our React app a message that says "Hello from server!" in a JSON object. The code below creates an endpoint for the route /api.
If our React app makes a GET request to that route, we respond (using res, which stands for response) with our JSON data:

Note: Make sure to place this above the app.listen function.
Since we've made changes to our Node code, we need to restart our server.
To do that, end your start script in the terminal by pressing Command/Ctrl + C. Then restart it by running npm start again.
And to test this, we can simply visit http://localhost:3001/api in our browser and see our message:

Step 5: Create your React frontend
After creating our backend, let's move to the frontend.
Open another terminal tab and use create-react-app to create a new React project with the name client:
npx create-react-app client
After that, we will have a React app with all of its dependencies installed.
The only change we have to make is to add a property called proxy to our package.json file.
This will allow us to make requests to our Node server without having to provide the origin it is running on (http://localhost:3001) every time we make a network request to it:

Step 6: Make HTTP Requests from React to Node
Now that we have a working React app, we want to use it to interact with our API.
Let's see how to fetch data from the /api endpoint that we created earlier.
To do so, we can head to the App.js component in our src folder and make an HTTP request using useEffect.
We will make a simple GET request using the Fetch API to our backend and then have our data returned as JSON.
Once we have the data returned to us, we will get the message property (to grab our greeting that we sent from the server) and then put it in a state variable called data.
This will allow us to display that message in our page if we have it. We are using a conditional in our JSX to say that if our data is not there yet, show the text "Loading...".


Step 7: Deploy your app to the web with Heroku
Finally, let's deploy our application to the web.
First, within our client folder, make sure to remove the Git repo that is automatically initialized by create-react-app.
This is essential to deploy our app, because we are going to set up a Git repo in the root folder of our project (react-node-app), not in client:

cd client
rm -rf .git

When we deploy, both our Node backend and React frontend are going to be served on the same domain (i.e. mycoolapp.herokuapp.com).
We see how our requests are being handled by our Node API, so we need to write some code that will display our React app when it is requested by our user (for example, when we go to the home page of our app).
We can do this back in server/index.js by adding the following code:

This code will first allow Node to access our built React project using the express.static function for static files.
And if a GET request comes in that is not handled by our /api route, our server will respond with our React app.
This code allows our React and Node app to be deployed together on the same domain.
Then we can tell our Node App how to do that by adding a build script to our server package.json file that builds our React app for production:
// server/package.json

I would also recommend providing a field called "engines", where you want to specific the Node version you are using to build your project. This will be used for deployment.
You can get your Node version by running node -v and you can put the result in "engines" (i.e. 14.15.4):

After this, we're ready to deploy using Heroku, so make sure you have an account at Heroku.com.
Once you are signed in and are looking at your dashboard, you'll select New > Create New App and provide a unique app name.
After that, you'll want to install the Heroku CLI on your computer so you can deploy your app whenever you make any changes using Git. We can install the CLI by running:
sudo npm i -g heroku

Once that's installed, you will log in to Heroku through the CLI using the heroku login command:

heroku login

Press any key to login to Heroku
Once you have logged in, just need to follow the deployment instructions for our created app in the "Deploy" tab.
