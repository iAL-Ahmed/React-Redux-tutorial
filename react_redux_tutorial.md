##Getting started with React    - By Issaq Al-Ahmed

Hey reader! Thanks for taking the time to read over this tutorial! It is still in it's early stages and I am excited to 
get some feedback. Feel free to make note of: things you like, thing you don't like, grammatical and/or technically 
errors, and anything else you feel would be helpful to me.

I hope you find this useful!

-Issaq

####What is React?

   React is a JavaScript component library made by Facebook. It acts as the V in MVC as it purely involves 
   visual components. As such it is pairable with just about any controller and model layer in other frameworks. 
   (React - Angular, React - Backbone, ect).
    
    
####Why use React (and when)

   React is a framework that focuses on the separation and componentization of concerns within your app. Any 
   code that is written within your component is locked in within that component and will not affect any other 
   component or state unless explicitly made to do so. This makes React an awesome choice for creating apps that have a 
   lot of moving parts that work independently of one another. 
   
   Another huge advantage of React compared to other similar frameworks/libraries (Angular, Ember, ect) is its performance.
   In the case of Angular there has always been a huge problem when it came to scalability. Angular works by adding a watch to
   every single item it sees on a component state. So as you can imagine if you have a super large application with many
   items being watched you were bound to run into some amount of performance issues as each watch cycle had to check x 
   number of variables for changes. React takes a different approach to the mass swarm of watches and opts for a single 
   smarter watch. This is done by making a finger print of your state on each component which only changes when something
   within that state changes. Thus you can get the same result without having to look at each variable independently. 
    
   A prime example of a case where React was a great choice was on Facebook's own core app. As there are tons of components
   working at the same time on that page (chat, alerts, the scrolling feed, settings toolbars, ect). So performance and 
   extensibility are vital!
   
####Time for some history!
    
   React actually came out of a need to fix the alerts icon on the top right of the main Facebook page. They were 
   constantly fighting with this feature because every time something else on the page changed it somehow affected this 
   component. This would result in the icon incorrectly displaying that a user had a new message/comment/or some 
   notification when they really didn't. Thus the Facebook team went to work on a solution that would completely isolate
   this feature and potentially any other feature such that it would never be affected by other changes on the page. The
   end result was the first version of React, a library for making their new "Flux" pattern work.
   
  
  
_____________________________________
   
###That's cool, so what are we going to do?

For this tutorial we are going to be making a very simple app where we click a button and see the text on the screen 
change. Every step in the process will be covered in detail including setting up your testing framework. The main goal 
of this tutorial set you up with all the truly necessary information needed to build most React Redux apps. As much 
cruft has been removed as possible and you will not see a shameless plug for my github account here!

####Note: 
I am not going to go over common JS syntax or common development tools like NPM. This assumes a basic understanding of 
web development. If I do not provide an explanation or links for something new or unclear to you, please google it. 
There is no shame in looking for answers!
*************************************   
   
###Getting started

Let's start by making our app directory and cd'ing ourselves in

```
mkdir my_react_app
cd my_react_app
```

We will now need to get the project ready for some dependencies by using:

```
npm init
```

Hit enter until the prompt asks "Is this ok? (yes)", then confirm. We can always change this later if needed. This 
command should create your package.json file correctly.

Next we will need to get our testing framework set up so we can test our future code.

```
npm install -g jasmine
```

----


####Optional: 
You may also want to install Jasmine locally to ensure that you can run tests should you share this development
code.

```
npm install --save-dev jasmine
```

You can then create and alias that refers to this local copy of Jasmine so all we need to type in to the console is Jasmine:
```
alias jasmine=<PATH_TO_MY_REACT_APP>/node_modules/jasmine/bin/jasmine.js
```
Now the Jasmine cli tool will work with your local (in your project dependencies) Jasmine.


----

###Setting up your testing

******************
####Note:
This testing section does not show you the details of how you write Jasmine tests for React apps.
It is on my todo list along with rewriting this section to use the Mocha testing framework instead of Jasmine. 

The info here is still useful and will show you how to set up Jasmine for your standard web-app. 
******************

This will install the Jasmine cli tool which we can use to run our test and set up our tests.

Now run:

```
jasmine init
```

This will give you a `spec` directory with a nested `support` directory and a `jasmine.json` inside that:

    spec directory
    |___support directory
         |___jasmine.json
      
The Jasmine.json file is the config file that Jasmine will read to make the magic happen.

By default it looks like this:
```
{
  "spec_dir": "spec",
  "spec_files": [
    "**/*[sS]pec.js"
  ],
  "helpers": [
    "helpers/**/*.js"
  ],
  "stopSpecOnExpectationFailure": false,
  "random": false
}
```

As you can see this is a plain old JavaScript object with various properties that tells Jasmine what to do.

 - "spec_dir" is literally the directory where your tests live.
 - "spec_files" is the property that will tell Jasmine how to read the spec files from the rest of the files in the spec
 directory.
 - "helpers" is the property that tells Jasmine where to find the helper files so that they can be included when the tests
 run.
 - "stopSpecOnExpectationFailure" is a property that tells Jasmine whether or not it should stop on the first failure it 
 finds or not.
 - "random" is the property that tells Jasmine whether or not it should run the tests in random order or sequentially.
 
      
Now

```
cd spec
```

from here you may add a spec file to the spec directory for your tests.

For example:
```
touch test_spec.js
```

and type this into test_spec.js

```
describe('this is a test', function(){
    it('this really is a test', function() {
        expect(true).toBe(true);
    });
});
```


Per the default configuration of the jasmine.json, Jasmine will look up all files ending with "spec.js" in your spec 
directory and run the tests in them.

For example, test files with names that look like this:

*   cat_list_spec.js
*   cheese_for_bees_spec.js
*   swank_view_controller_spec.js

****************************************************

Great, now that you've got a dummy test file going, you just need to run this command in your project directory:
```
cd ..
jasmine
```

You should see the single test run and it should be green! 

***************************************************
####Note:
Jasmine is able to run in a browser to give you better visibility. That being said the Jasmine npm module does not 
come with this ability out of the box. You would either have to pull the "spec-runner" code out of the Jasmine 
stand alone zip file download or use a third party wrapper that typically relies on gulp. Gulp is likely to be your 
task runner of choice so this works out pretty good. I would personally suggest one use the "gulp-jasmine-browser" 
module to set up your tests to run. This takes care of any concerns about the spec runner and any potential ambiguity
when setting up your task runner.

It looks like this:

![Image of jasmine_spec_runner](http://blog-jmtalarn.rhcloud.com/wp-content/uploads/2016/10/2016-10-15-01_56_10-Jasmine-Spec-Runner----Microsoft-Edge.png)

<br>

####Additional fun facts:
If you should get Jasmine through a ruby gem or python egg, it will be pre-equipped with the Jasmine spec runner!


------------------------------------------------------
####Optional 

You can also assign a more general command with npm to run your tests.

In your package.json add this under your scripts property:
```
"test": "jasmine",
```
so you should end up with something like this:
```
"scripts": {
    "test": "jasmine"
  },
```

and you can now run this command to run your tests
```
npm test
```
------------------------------------------------------


###Setting up the File Structure and Build Chain

Time to the first bits of our application file structure!

```
mkdir src
cd src
mkdir actions components containers reducers constants store
```
        
This is the typical file structure configuration you would see in a React Redux app.

Now we are going to download our application dependencies and setup our build chain! 

*************************************************
####Build chain?

For this project we will be using webpack as our build chain tool. The good people at webpack can do a much better job 
of explaining what it does and why it is an awesome build chain tool.

In a nutshell webpack is a tool that can grab all of your code, and its dependencies, and then build it into
a single, compiled, JavaScript file. When we serve up a single file, as opposed to many, we make it easier to serve our 
app up to users when they visit your website by literally having less things to send over.

Official webpack explanation:
https://webpack.js.org/concepts/

*************************************************

Let's install webpack and all of the other key components for our app: React, Redux, prop-types, and babel.

```
npm install --save-dev webpack babel-preset-react babel-preset-es2015 babel-preset-stage-0 babel-loader babel-core

npm install --save react react-dom prop-types
```

All the packages that have "babel" in the name will be used as part of our webpack build chain to transpile (meaning to 
convert to a different version) our JavaScript. After webpack has run our end product is still JavaScript but translated
JavaScript that will conform to JavaScript standards that work with older browsers. 

Prop-types is a tool we will be using to specify the props that our React components will be able to use. That will make
more sense once we get to making our React components.

*********************************
#####NOTE:
prop-types was previously included as a part of React but has since been spun out into it's own npm module. So if you 
see examples elsewhere that have prop-types being included from React that is why.
*********************************

```
npm install --save updeep
```

Updeep is a very helpful tool that we will use later to deeply extend JavaScript objects. Don't worry we'll get to it later.
 
Let's make a dummy index.js file, a webpack configuration file, and a babel configuration file.

- this assumes we are still in /src
```
touch index.js
cd ..
touch webpack.config.js
touch .babelrc
```

In your webpack.config.js we will want to add:

```
module.exports = {
    entry: "./src/index.js",
    output: {
        path: __dirname,
        filename: "bundle.js"
    },
    module: {
        loaders: [
            { test: /\.js$/, loader: "babel-loader" }
        ]
    }
};
```

 
This is the configuration code for webpack. It tells webpack where key application files live and what actions to 
perform on them.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This code **format** can be found on the webpack getting started page: https://webpack.js.org/concepts/


The properties are for:

*   entry - is the first js file to be run in your app.
*   output - tells webpack where to place your processed code and by what name to call it.
*   module - contains a list of plugins that will be run against your code when you tell webpack to run.

and in the .babelrc we will add:

```
{
  "presets": ["es2015", "stage-0", "react"],
}
```

*******************************************************
####Note:
The dot out front of .babelrc denotes that this is a hidden file. So if you don't see .babelrc when you type in
the ls command that just means it is hidden. It is still there however!
*******************************************************

The .babelrc file is a config file specifically for babel. The preset field represents the type of compiler(s) needed for 
the various forms of JavaScript (ES6, es7, jsx, ect) that may be in your app. Think of them as plugins. In this case we 
wanted es2015, stage-0, and React.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;es2015 - is used for making translations from newer JavaScript versions to ES5.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stage-0 - is used for making translations of the newest JavaScript tools, even if 
hey have not yet been standardized.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;react - is used for t-cific code to browser readable ES5.
    
Now we should be able to simply run:
```
webpack
```

and we will see a file called bundle.js get made. We are not expecting to see much in the bundle file right now. Later 
we will start to see that the bundle file will include all of your application code. 
    
*******************************************************

####Pro tip!

If you run into pathing errors when you run the webpack command like this:
```
ERROR in Entry module not found: Error: Cannot resolve 'file' or 'directory' ./src/index.js in /Users/pivotal/workspace/react_gettings_started_jasmine
```

Start troubleshooting by running
```
npm install
```

It sounds strange, but believe it or not the package.json can affect webpack. If there are any syntax errors in your
package.json you will likely run into errors like what was mentioned above.

Crazy right?

********************************************************

###Setting up React and Redux

*.* * * * * * * *
####TODO:
Insert some magical image showing the flow we will be seeing in this app. 

*.* * * * * * * *


##React

First we need 

```
cd src
touch index.html
```

The index.html file is literally the first thing that the browser is going to see when it loads your app. So inside
of this file we will add something that looks like this:

```
<!doctype html>
<meta charset="utf-8">
<script async src="../bundle.js"></script>
<div id="root"></div>
```

Seeing as we be using React as our primary means of DOM structure we have written the bare minimum html to make your app
work. Don't be concerned about the lack of a head or body tag. They are not required and this does, in fact, work just 
fine ☜(ﾟヮﾟ☜).

*************************

####Important!
It is really important that you add a class or id to an element in your index.html. In our case we used `root` as our id.
This selector will be needed to tell React where to load the first React component of your app! Without loading your 
first component the rest of your app will not load!

*************************

####React Component Data Control
Before we make our first React component, it is important that we cover how React components manage their data.

In a React component there are two types of data that control a component: props and state. Props are set by the parent 
when the child component is rendered. The props data is then fixed throughout the lifetime of a component. For data that can 
change over the use of a component, we have to use state.

It is worth noting that for the purposes, and simplicity, of this tutorial we will not be using the React component 
state. However, I would strongly encourage a quick read through of React docs on this topic as you are bound to see it 
used in larger apps.

https://facebook.github.io/react-native/docs/state.html *

*Yes I know this is react native but it is literally the same code and these docs are way more concise. 


************************

You may remember when we were setting up webpack that we made a file called index.js and then set it as our application's
entry point. We will now make index.js render our first React component!

Inside index.js write some code like this:

```
import React from 'react';
import ReactDOM from 'react-dom';

import Application from './components/Application';

ReactDOM.render(<Application text="Hello World!" />, window.root);
```

************************
####Is that HTML in our JavaScript!?

Yep! This is what we call JSX (JavaScript XML) syntax. JSX files are basically just JavaScript files with HTML in them.
In older React apps you may see JSX files instead of just JS files. However, Thanks to tools like babel we do not need 
to worry about using the JSX file extension. JS is transpiled just like JSX allowing us to write JSX syntax in our 
JavaScript code.
************************

In this code we are first importing (an ES6 term) React, the react-dom tools (that help React manipulate the DOM), and 
our primary React component (Application). We are then rendering the Application component to the DOM selector we specified
on the index.html (```id=root```) and passing along a prop called text (that is set to "Hello World!").

Now we need to have something to actually render on our page, so let's make our Application component!

```
cd components
touch Application.js
```

and let's now add this code to the Application.js

    import React from 'react';
    import PropTypes from 'prop-types';
    
    const Application = ({text}) => {
        return <p>{text}</p>
    };
    
    Application.propTypes = {
        text: PropTypes.string
    };
    
    export default Application;

Here, again, we see that we are importing in our dependencies but we are also exporting some code (exporting default).

Also, remember when we installed prop-types? This is how we will be using it to define what props our react components 
can accept, otherwise known as "typechecking". First we define the name of the prop, then we use prop-types to define the
data type of the prop.
 
Typechecking is NOT required in React but it is strongly encouraged. It gives you that little bit extra of security to 
ensure your code behaves correctly as well as to give you some insight when it doesn't (by throwing specific errors).

Do be aware that ```Application.propTypes``` is NOT the same as ```PropTypes.SOME_DATATYPE```. We simply define a variable
on the Application React component to then hold the object that we define our prop types in. The other prop-types with the 
upper-case P is the actual prop-types module we imported.
 
It is also worth mentioning that you can also require properties for your components. This is done by writing something 
like: ```text: PropTypes.string.isRequired```

******************************************

####Note:
In ES6 JavaScript you will see two main ways of exporting code:
    
export default - Which you use when exporting a single piece of code.

```
//------ myFunc.js ------
export default function () { ... };

//------ main1.js ------
import myFunc from 'myFunc';
```    
    
export - Which you use when you are exporting multiple pieces of code.
```
//------ lib.js ------
export function zero() { ... }
export function one() { ... }
export function two() { ... }

//------ main.js ------
import { one, two } from 'lib';
```

Really you could just default to the second option, but this helps keep your code easier to import.

It is also worth noting that we are using ES6 function declarations in this tutorial. Fat arrow functions are an ES6 short 
hand for a function that is bound to the local context. 

So if you see:
```
() => { SOME CODE }
```
it is the same as:
```
function () { SOME CODE }.bind(this)
```
     
******************************************
 
We are exporting an anonymous function that takes in an argument (an object with a text prop) and returns the html 
that displays the text prop. 

Great, now we just need to bundle up this code with webpack, start up a server, and load the app up in a browser!
 
run:
```
cd ../..
webpack
python -m SimpleHTTPServer
```

for this example we are using a python simple server to serve our code up to the browser.

Now let's open up a browser and go to ```localhost:8000/src``` (the url that our server is sending our app). We should now see
"Hello World!" on the page!

So to sum up what is going on:
1. The browser is loading our index.html which has a script tag that loads the bundle.js file (produced by webpack). 
The index.html also contains the root element where we can render our React components.
2. The index.js and Application.js are loaded as part of the bundle.js. The index.js is the entry point for 
our JavaScript app. The index.js renders the Application component and then passes the text "Hello World!" in as a prop.
3. Once rendered, the Application component should display the text we passed in to it ("Hello Wolrd")!

Congrats! We have made a React app!

But we are not done yet! Let's get Redux involved!

*************************************
###Woah! What is Redux!?

Redux is a global state container for JavaScript apps which can work with a number of frameworks and libraries. Similar 
to React, Redux has a one way data flow and as such pairs great with React. For our purposes Redux will act as the 
controller model layer (remember that React acts as the View). 

In more detail Redux works on the idea of state containment. This means having an application with a global frontend store.
So as you use your app you can persist the state of your activity without having to worry about losing it when you move
from one page/component to another. For example, say I closed a form that was filled in but not submitted. Normally that
data would be gone to the cyber winds but if we use Redux to create a global store (a "state container") we can then back 
that information up and come back to it later from anywhere in the app. You could always just make your own method of 
storing this this kind of information, but Redux gives you the tools to do this in a reasonable and scalable way.

###That's cool, but why?

Simply put, to help you avoid anti-patterns. Think about it this way, without some sort of app wide state container you 
are more likely to have to have a component modify another component directly. While you can probably keep this up for a 
bit you will almost certainly run into issues as your app grows. One component relies on another, and then that one relies
on even more components. You are going to have some serious spaghetti code and hard to trace data in no time. By 
removing the need to do this, you are likely to write cleaner code which is ~*scalable*~.

*************************************

```
npm install --save react-redux
cd src
```
 
In addition to the React component state, with the inclusion of Redux we are now given access to the global/application 
Redux state. 

It is very possible to be unsure which state to use as you develop so here are the general use cases for each.

* React component state is great for ephemeral changes (things that will need to live only as long as the component). 
* Redux state is great for frontend persistent state ("I will be coming back to this" type of data).

In any case, let's start prepping the app for Redux!

First things first, let's modify the index.js file to look something like this:

```
import React from 'react';
import ReactDOM from 'react-dom';

import Application from './components/Application';
import store from './store/store';

ReactDOM.render(<Application store={store} />, window.root);

```

As you can see we have added an import for store to the index.js. Our store will be our creation point for our global 
state store.

So let's create the store file

```
cd store
touch store.js
```

now add this to that file.
```
import { createStore } from 'redux';
import reducers from '../reducers/words';

const store = createStore(reducers);
export default store;
```

createStore is a function that comes from Redux that allows for the creation of a global store. To manipulate the store, 
we use a specialized function called a “reducer”. Reducers act as a logic joining point and are responsible for 
triggering actions.

Of course we do not yet have any reducers (which you can have many of) so let's add this in to the mix.

```
cd ../reducers
touch words.js
```

Now let's write this into our words.js
 
```
import u from 'updeep';

const reducer = (state = {text: 'first words'}, action) => {

    switch (action.type) {
        case 'ADD_WORDS':
            return u({text: action.text}, state);
        default:
            return state
    }
};

export default reducer
```

A reducer is a function that takes a state and an action as arguments. The reducer then runs the action type against a 
series of switch conditions. Based on the type of action (also known as an action-type) it will perform some kind of 
action on the application state store. In this case if an action-type called ```ADD_WORDS``` is found then an updated
clone of the state will be returned. If ```ADD_WORDS``` is not found then the original state is returned.

We do not interact with reducers directly so just think of this as a tool you will be feeding to Redux so that it knows
how you want your app to react to action calls. See what I did there?...hah.

Also, as you can see we did indeed come back around to using updeep! We will be using it to make deep copies of our state.

---------------------------------------
####Why do we make deep copies of state in our reducers? 
 In Redux it is considered bad practice to modify your state directly in your reducers. To my dismay, no reason for why 
 this is considered bad practice is ever formally given in the official Redux documentation. Only after a good deal of 
 research I was able to piece together a reasonable explanation.
 
 React Redux apps have the ability to be debugged using a method known as "time travel debugging". In a nut shell, time 
 travel debugging allows you to move in between states while debugging your app. In order to be able to use this method 
 of debugging you need to be able to separate your state changes as separate objects (i.e. different copies). So if you 
 do not make copies of state when applying changes you will not be able to do time travel debugging.
 
 Here is a link to a stack overflow discussion about the need for immutability for Redux application state.
 https://github.com/reactjs/redux/issues/328
 
 Also here is a link with some more detailed info about time travel debugging:
 https://code-cartoons.com/hot-reloading-and-time-travel-debugging-what-are-they-3c8ed2812f35

---------------------------------------


Remember this line from store.js?
```
var store = createStore(reducer);
```

Yeah, that is where we hand things off to Redux!

Now we have one quick modification we SHOULD do but are not required to do. This is something that helps against typos 
down the road.

```
cd ../constants
touch action-types.js
```

Here we are going to make a table of constant variables that we can call upon when we need to refer to the names of our 
various actions.

Add this:

```
export const ADD_WORDS = "ADD_WORDS";
```

So now if we return to our words reducer and change it to look like this:
```
cd ../reducers
```
```
import * as types from '../constants/action-types';
import u from 'updeep';

const reducer = (state = {text: 'first words'}, action) => {

    switch (action.type) {
        case types.ADD_WORDS :
            return u({text: action.text}, state);
        default:
            return state
    }
};

export default reducer
```

We now are using the table! If you missed that we simply imported the action-types list and then changed our key for the 
switch case to use the value from our action-types file.

In the future we can just add our action names to action-types and call upon the action-types wherever we need them. We 
will see more of this once we get to our containers.

Ok!

Now that we have got our stores set up we can move on to hooking in Redux into our React components.

First, let's get started with making a component that we will hook up into Redux
```
cd ../components
touch TextComponent.js
```

in TextComponent write this:

    import React from 'react';
    import PropTypes from 'prop-types';
    
    const TextComponent = ({text}) => (
        <div>
            {text}
        </div>
    );
    
    TextComponent.propTypes = {
        text: PropTypes.string
    };
    
    export default TextComponent

This is a very simple functional stateless React component. We import React and PropTypes, we create a function to be 
read by React, define what properties we expect this component to be made with (in the form of html 
attributes), and return the html we want this component to render. The component is simply rendering
some text that will be passed in as a prop at creation time (for the component).

-------------------------------------------
###Functional?

So this can be a bit confusing at first, but React has gone through some changes since it was first released. Long story
short, there are a few different notations you will see used to write a React component. There are some differences 
between them but nothing too major. If you are planning on using the 
[React life cycle](https://Facebook.github.io/react/docs/react-component.html) then you will have to use one of the 
class oriented notations (options 1 and 2);
 
For example: 

1. A now-deprecated React-sourced createClass method

        var Component = React.createClass({
            // this.props is available 
            render: ( some html )
        })

2. an ES6 class definition
    
        class Component extends React.Component {
          render() {
            // this.props is available 
            return ( some html );
          }
        }

3. a function (also known as a functional component)
    
        export const Component = (props) => {
            // props are passed in ^
            return (
                some html
            );
        };

####Also note!
Components must have capitalized names! Otherwise they just wont render and everyone will be sad.

-------------------------------------------
Now we need a container.

###Container?

What is a container? Well that requires a little explanation:

In a plain React app we would simply make a component and render it from the Application.js file. However when we use 
Redux we need to add a layer in front of the components to make the connections between our React components and Redux.
We call these pieces containers. Containers are written using React components that wrap around your other React 
components, thus "containing" the components in your app.

But how though? Let's write out our container and go over it.

```
cd ../containers
touch TextComponentContainer.js
```

and let's write this in it:
```
import React from 'react';
import PropTypes from 'prop-types';
import { connect } from 'react-redux';
import TextComponent from '../components/TextComponent';

export const TextComponentContainer = (props) => {
    return (
            <TextComponent text={props.text} />
        );
};

TextComponentContainer.propTypes = {
    text: PropTypes.string
};

const mapStateToProps = function(store) {
    return {
        text: store.text
    };
};

export default connect(mapStateToProps)(TextComponentContainer);
```

This can be a bit hard to follow so let's clarify what we did:

1. Firstly we are importing React, React PropTypes, connect from react-redux, and our component (TextComponent).
2. Next we are creating a functional React component! Yes, we are using React as a means of setting up our containers 
(which contain our components).
3. Now we need to make our bindings between React and Redux. We are going to be passing mapStateToProps into the connect
function call on the last line. Connect expects a function that takes a store and then returns an object. 
4. The connect function will return a function that we can use to make a binding between the Redux store props specified 
in the return value of the mapStateToProps function.
5. We then invoke the returned function from the connect function and pass in the component we want to make the binding 
to, which is TextComponentContainer in this case.
6. Tada! When the textComponent is rendered we can now pass in the state properties as props!

*********************************
###Note:
The container does not explicitly need to be a functional (or regular) React component. We could actually just make a 
mapStateToProps function and then call the connect function and still be able to pass values in to a component as props.
The only reason we don't do this here is that by making this into a React component it gives us the ability to easily 
re-use this component in many places in the app.
*********************************

Now, because containers are just React components that wrap React components we do need to render them.

```
cd ../components
```

Edit your Application.js to look like this:

```
import { Provider } from 'react-redux'
import TextComponentContainer from '../containers/TextComponentContainer'
import React from 'react';
import PropTypes from 'prop-types';

const Application = (props) => {
    return (
            <Provider store={ props.store }>
                  <TextComponentContainer />
            </Provider>
    )
};


Application.propTypes = {
    store: PropTypes.object
};

export default Application;
```

This will now render your container.

But wait? What is this "Provider" thing?

Provider is a component supplied by react-redux that allows components "connected" to Redux to have access to the 
application store. 

Remember when we created the store in the index.js? The store was then passed into the application component as a prop. 
Well here it is!

Now our container has access to the application store!


##Actionssss

Something is seems off? Why yes that is right, we have yet to give a way to actually set or change our application state!
Seeing as our application state now lives with Redux we must now add in an action to set the store.

Do note that it is very important to know that when you are using actions that you are changing the application state 
store, not the component state. If you confuse the two you can possibly end up with unintentional worlds existing!

```
cd ../actions
touch add-words-action.js
```

now add this:
```
import * as types from '../constants/action-types';

export const addWords = (text) => {
    return {
        type: types.ADD_WORDS,
        text
    }
};
```

Many would refer to this as an "action creator" due to the fact that a function call is needed to actually get the action
object. Really, you could just inline the object wherever you need to call for a change, but this way we can reuse the
action in many places and not have to depend on a bunch of boiler plate.

```
cd ../containers
```

The action that we just made will be used within our containers. So in our case we can modify our TextComponentContainer
to look like this:

```
import React from 'react';
import PropTypes from 'prop-types';
import { connect } from 'react-redux';
import { bindActionCreators } from 'redux';
import TextComponent from '../components/textComponent';
import * as Actions from '../actions/add-words-action.js'

export const TextComponentContainer = (props) => {
    return (
            <TextComponent text={props.text addWords={props.actions.addWords} />
        );
};

TextComponentContainer.propTypes = {
    text: PropTypes.string,
    actions: PropTypes.object
};

const mapDispatchToProps = (dispatch) => ({
    actions: bindActionCreators(Actions, dispatch)
});

const mapStateToProps = function(store) {
    return {
        text: store.text
    };
};

export default connect(mapStateToProps, mapDispatchToProps)(TextComponentContainer);
```

As you can see we have added mapDispatchToProps. In a similar fashion to mapStateToProps, mapDispatchToProps binds our 
actions to our container props. You will also notice that we included ```addwords={props.actions.addWords}``` to our 
child component we are rendering. There, using the action that we bound to our container props, we are passing the addWords
action to our child component. Our child component can now dispatch the addWords action! Let's make our way to TextComponent.

```
cd ../components
```

And now we can spruce some things up with the action we are now passing in as a prop in out TextComponent:

    import React from 'react';
    import PropTypes from 'prop-types';
    
    const TextComponent = ({text, addWords}) => (
        <div>
            {text}
            <button type="button" onClick={ () => addWords('yaaaay') } >Click me!</button>
        </div>
    );
    
    TextComponent.propTypes = {
        text: PropTypes.string,
        addWords: PropTypes.func
    };
    
    export default TextComponent

As you can see we have now acknowledged that we are getting our action as a prop by adding it to our proptypes and 
functional component. From there we are then able to bind the function to a button by wrapping it in an ES6 fat arrow 
anonymous function.
 
###But does it work?

Time to find out if we have completed the circle and can now change our state.

```
cd ../..
```

Now from our project directory let's run our webpack command
```
webpack
```

We will now get a newly compiled version of the app with all of our changes that we can then serve up with our simple
http server:

```
python -m SimpleHTTPServer
```

Now if we go to our web browser and go to localhost:8000 we should see our app. It is just a word and a button next to
it. So now if we click this button we should see the word change to "yaaaay".

Congrats! We now have a working pattern for our React Redux app that we can use! -victory fanfare-

##Recap!

Alright, so obviously there is a lot to do and know in order to be most effective when writing your React Redux app, so
let's list things out in order just to help give a high level overview of what you just did.

1. We set up our app working environment.            
  - made our project directory ```mkdir my_react_app```  
  - ```npm init``` our project directory
  
2. We then set up our testing framework
  - installed Jasmine
  - ```jasmine init``` in our working environment
  - made our first spec file ```touch test_spec.js```
  - wrote a dummy test
  - ran jasmine to make sure the test worked

3. We created our app file structure ``` mkdir src, mkdir actions components containers ...ect ```

4. Installed our dependencies
  - ```npm install --save-dev webpack ...ect```
  - ```npm install --save react ...ect```
  
5. Configured webpack and babel to build our app with an entry point of index.js!
  - created our entry point for the app```touch index.js ```
  - created our webpack config file ```touch webpack.config.js ```
  - created our babel config file ```touch .babelrc```
  - ran webpack to generate our bundle.js file 

6. We wrote our index.html to give us a place to load our app.
7. We took the index.js file that we made as our entry point for webpack and had it render our main application component.
  - ```ReactDOM.render(<Application text="Hello World!" />, window.root);```
  
8. We defined our Application.js component (to be loaded in the index.js).
  - ```touch Application.js```
  
9. We then confirmed that we could compile our project by running webpack again now that we had a component.
  
10. Began setting up Redux by creating and adding a store to our index.js
  - ```import store from './store';```
  - ```touch store.js```
  
11. We created our first reducer called words.js

12. We added the Redux provider to the Application.js file to expose our global store!
  - ```<Provider store={ props.store }>```

13. We created an action-types file to add naming rigidity to our actions (constant names to refer to the actions).

14. After that we made our first presentation component called TextComponent (one that will actually show information and be rendered inside of Application.js)

15. Now we needed a container to bind Redux to our React components so we made TextComponentContainer.js.
  - here we bound our state to the props of the components ```export default connect(mapStateToProps)(TextComponentContainer);```
  
16. We created an action called add-words-action.js that updates our word on global state (store)

17. Next we registered our action with our container so we could call it from our components.
  - ```export default connect(mapStateToProps, mapDispatchToProps)(TextComponentContainer);```
  -  <TextComponent text={props.text} addWords={props.actions.addWords} /> inside our container
  
18. Finally we did one last webpack build and served our app up using a simple python server. Bon appétit! 


#Woo! We did it!


<br><br><br><br><br><br>

