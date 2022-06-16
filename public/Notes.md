## Modular Code
Modular code is code that is separated into segments (modules), where each file
is responsible for a feature or specific functionality.

React makes the modularization of code easy by introducing the component
structure. Standard practice - givee each component their own file.
```jsx
function ColoradoStateParks() {
  return <h1>Colorado State Parks!</h1>;
}

## Import and Export
On a simplified level, the `import` and `export` keywords let us define
variables in one file, and access those variables in other files throughout our
project.

### Exporting Variables
Exporting any variable — whether that variable is an object,
string, number, function, or React component — allows us to access that exported variable in other files.

#### Default Export Syntax
We can only use `export default` once per file. This syntax lets us export one variable from a file which we can then import in another file.

// src/parks/howManyParks.js
function howManyParks() {
  console.log("42 parks!");
}
export default howManyParks;

We can now use the 'import' keyword to access that variable in another file.

// src/ColoradoStateParks.js
import React from "react";
import howManyParks from "./parks/howManyParks";

function ColoradoStateParks() {
  howManyParks(); // => "42 parks!"

  return <h1>Colorado State Parks!</h1>;
}

If you need to an export default your variable, but your are using a library that exports the same variable name, you can change yours to whatever you want. Otherwise, use it sparingly for the sake of debugging.
// src/ColoradoStateParks.js
import React from "react";
import aDifferentName from "./parks/howManyParks";

function ColoradoStateParks() {
  aDifferentName(); // => "42 parks!"

  return <h1>Colorado State Parks!</h1>;
}

#### Named Exports
With named exports, we can export multiple variables from a file:
// src/parks/RockyMountain.js
const trees = "Aspen and Pine";

function wildlife() {
  console.log("Elk, Bighorn Sheep, Moose");
}

function elevation() {
  console.log("9583 ft");
}

// named export syntax:
export { trees, wildlife };

### Import
'import' keyword lets us take variables that we have exported and use them in other files.

The `import * from` syntax imports all of the variables that have been exported
from a given module. This syntax looks like:
// src/ColoradoStateParks.js
import * as RMFunctions from "./parks/RockyMountain";

console.log(RMFunctions.trees);
// => "Aspen and Pine"

RMFunctions.wildlife();
// => "Elk, Bighorn Sheep, Moose"

RMFunctions.elevation();
// => Attempted import error

In the example above, we're importing all the exported variables from file
`RockyMountain.js` as properties on an object called `RMFunctions`. Since
`elevation` is not exported, trying to use that function will result in an
error.

We are using the **relative path** to navigate from `src/ColoradoStateParks.js`
to `src/parks/RockyMountain.js`. Since our file structure looks like this:
└── src
     ├── parks
     |   ├── RockyMountain.js
     |   ├── MesaVerde.js
     |   └── howManyParks.js
     ├── ColoradoStateParks.js
     └── index.js

#### Importing Specific Variables

The `import { variable } from` syntax allows us to access a specific variable by
name, and use that variable within our file.

We are able to reference the imported variable by its previously declared name
// src/ColoradoStateParks.js
import { trees, wildlife } from "./parks/RockyMountain";

console.log(trees);
// > "Aspen and Pine"

wildlife();
// > "Elk, Bighorn Sheep, Moose"

We can also rename any or all of the variables inside of our `import` statement:
// src/ColoradoStateParks.js
import {
  trees as parkTrees,
  wildlife as parkWildlife,
} from "./parks/RockyMountain";

console.log(parkTrees);
// > "Aspen and Pine"

parkWildlife();
// > "Elk, Bighorn Sheep, Moose"

// src/ColoradoStateParks.js
import React from "react";  //Here, we are referencing the React library's default export (located inside of the 'node_modules' directory.
import howManyParks from "./parks/howManyParks";
import MesaVerde from "./parks/MesaVerde";
import * as RMFunctions from "./parks/RockyMountain";

export default function ColoradoStateParks() {
  return (
    <div>
      <MesaVerde />
    </div>
  );
}

Full example from react-hooks-import-export
___________________________________________
function ColoradoStateParks() {
  return <h1>Colorado State Parks!</h1>;
}

___________________________________________
// src/parks/howManyParks.js
function howManyParks() {
  console.log("42 parks!"); //
}
export default howManyParks;

___________________________________________
// src/ColoradoStateParks.js
import React from "react";
import howManyParks from "./parks/howManyParks";

function ColoradoStateParks() {
  howManyParks(); // => "42 parks!"

  return <h1>Colorado State Parks!</h1>;
}

___________________________________________
// src/parks/MesaVerde.js
import React from "react";

function MesaVerde() {
  return <h1>Mesa Verde National Park</h1>;
}

export default MesaVerde;

_____________________________________________
// src/ColoradoStateParks.js
import React from "react";
import MesaVerde from "./parks/MesaVerde";

function ColoradoStateParks() {
  return (
    <div>
      <MesaVerde />
    </div>
  );
}

export default ColoradoStateParks;

_____________________________________________
// src/parks/RockyMountain.js
const trees = "Aspen and Pine";

function wildlife() {
  console.log("Elk, Bighorn Sheep, Moose");
}

function elevation() {
  console.log("9583 ft");
}

// named export syntax:
export { trees, wildlife };

_____________________________________________
// src/ColoradoStateParks.js
import { trees, wildlife } from "./parks/RockyMountain";

console.log(trees);
// => "Aspen and Pine"

wildlife();
// => "Elk, Bighorn Sheep, Moose"

______________________________________________
import * as RMFunctions from "./parks/RockyMountain";

console.log(RMFunctions.trees);
// => "Aspen and Pine"

RMFunctions.wildlife();
// => "Elk, Bighorn Sheep, Moose"

RMFunctions.elevation();
// => Attempted import error
In the example above, we are importing all the exported variables from file
`RockyMountain.js` as properties on an object called `RMFunctions`. Since
`elevation` is not exported, trying to use that function will result in an
error.

_______________________________________________________________________________-

##JSX Lab Notes:
##JSX
is declarative programming

const div = (
  <div id="card1" className="card">
    hello world
  </div>
);
ReactDOM.render(div, document.body);

React components return JSX:
function Tweet() {
  const currentTime = new Date().toString();

  // this returns JSX!
  return (
    <div className="tweet">
      <img src="http://twitter.com/some-avatar.png" className="tweet__avatar" />
      <div className="tweet__body">
        <p>We are writing this tweet in JSX. Holy moly!</p>
        <p>{Math.floor(Math.random() * 100)} retweets </p>
        <p>{currentTime}</p>
      </div>
    </div>
  );
}
Every function component you use needs to return one JSX element.
The entire return statement is wrapped in parentheses, so it's one 'chunk' of JSX code, with one top level element:
return <div className="tweet">{child elements in here}</div>;

##JSX is not a String and is not wrapped in quotes

##JSX can include JavaScxript, in-line by wrapping the JavaScript in curly braces.
<p>{ Math.floor(Math.random()*100) } retweets</p>
<p>{ currentTime }</p>

##JSX works with expressions, not statements
expressions have a return value, statemnts do not.
for example, you cannot use if statements
<h1 id="header">{if (true) {
  "Hello"
} else {
  "Goodbye"
}}</h1>
above is not valid JSX

ternary expressions do work!
<h1 id="header">{true ? "Hello" : "Goodbye"}</h1>

if you need to exress code with an if statemnt, you need to call another function within JSX
function Header() {
  function getHeaderText(isHello) {
    if (isHello) {
      return "Hello";
    } else {
      return "Goodbye";
    }
  }

  return <h1 id="header">{getHeaderText(true)}</h1>;
}

##A component can render another component using JSX
function Header() {
  return <h1>Hello</h1>;
}

function Page() {
  return (
    <div>
      <Header />
      <p>Some great content in here</p>
    </div>
  );
}

name of elements is lowercase
name of components is capitalized
This is how react differentiates the <Header> component from a normal HTML <header> element.

##A component must return one JSX Element
we can use any HTML element we normaly use to contain content.

function PlainDiv() {
  return <div>I am one line, so I do not need the parentheses</div>;
}

const Photo = () => {
  return (
    <figure>
      <img
        className="image"
        src="https://s3.amazonaws.com/ironboard-learn/sunglasses.gif"
      />
      <figcaption>Whoa</figcaption>
    </figure>
  );
};

const Table = () => (
  <table>
    <tr>
      <th>ID</th>
      <th>Name</th>
    </tr>
    <tr>
      <th>312213</th>
      <th>Tim Berners-Lee</th>
    </tr>
  </table>
);

function ParentComponent() {
  return (
    <main>
      <PlainDiv />
      <Photo />
      <Table />
    </main>
  );
}

All above have one returned JSX element

If you want a component to return multiple JSX elements that are not wrapped in a containing DOM element, React fragments (Links to an external site.) can help with that.

##JSX Property Names
JSX uses className instead of class
JSX uses htmlFor instead of for

##Props Basics
turn a React component into dynamic template using props.
A react component is a function that takes props as an argument and returns JSX.
components are dynamic in that they can describe a template of JSX in which variable data can be populated.

### Making Components Dynamic
3 components:
- `BlogContent` - contains the content of the blog post
- `Comment` - contains one user's comment
- `BlogPost` - the 'top level' React component, which is responsible for
  rendering both `BlogContent` and `Comment`

function BlogContent(props) {
  return <div>{props.articleText}</div>;
}

##Passing Information
props - units of information being passed down from a parent component to a child component.
Passing information from 'BlogPost' down to its child 'BlogContent':

function BlogPost() {
  return (
    <div>
      <BlogContent articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration." />
    </div>
  ); //We rendered the 'BlogContent', created a prop called 'articleText', then assigned a value of "Dear Reader: Bjarne ...

  //The assigned value is accessible from within 'BlogContent' as 'props.articleText'.
}

syntax for creating props is the same as writing attributes for an HTML tag.
For example, to assign a `<div>` an
id, we give it an attribute:
```html
<div id="card">Hello!</div>
```
To assign a **prop** to a **component**, we use the same syntax:

```jsx
function ParentComponent() {
  // passing prop to ChildComponent
  return <ChildComponent text="Hello!" number={2} />;
}

function ChildComponent(props) {
  // using the values of the text and number props
  return (
    <div>
      {props.text} {props.number}
    </div>
  );
}
But remember, this is JSX and not HTML!

##props expanded to better understand how data can be passed from component to component:
jsx

jsx
// BlogPost.js
// PARENT COMPONENT
function BlogPost() {
  return (
    <div>
      {/* BlogContent is being returned from BlogPost */}
      {/* Therefore, BlogContent is a child of BlogPost */}
      <BlogContent articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration." />
    </div>
  );
}

// BlogContent.js
// CHILD COMPONENT
function BlogContent(props) {
  console.log (props); // => { articleText: "Dear Reader: Bjarne Stroustrup has the perfect lecture oration." }
  return <div>{props.articleText}</div>;
}

The only way for a parent component to pass data to its child component is via **props**.

We can add as many additional props as we want by assigning them in the parent
component, and all of these props will be added as **keys on the props object** in the child component.

function BlogPost() {
  return (
    <div>
      <BlogContent
        articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration."
        isPublished={true}
        minutesToRead={1}
      />
  )
}

js
BlogContent.js
console.log(props);
// =>
  { 
    articleText: "Dear Reader: Bjarne Stroustrup has the perfect lecture oration.",
    isPublished: true,
    minutesToRead: 1 
  }

props that are strings don't use curly braces around values, but other data types (numbers, booleans, objects, etc) we need curly braces.

the ability to pass props down to a child component from a parent makes components really flexible. Expand on 'blogContent' component with the additional props:
jsx
function BlogContent(props) {
  console.log(props);

  if (!props.isPublished) {
    // hide unpublished content
    // return null means "don't display any DOM elements here"
    return null;
  } else {
    // show published content
    return (
      <div>
        <h1>{props.articleText}</h1>
        <p>{props.minutesToRead} minutes to read</p>
      </div>
    );
  }
}
We are using conditional rendering to only display blog content if it is published, based on the 'isPublished' prop.

##expanding our application
add comment component:
jsx
function Comment(props) {
  return <div>{props.commentText}</div>;
}
this component, when used, will display content that is passed down to it, allowing us to pass different content to multiple "Comment' components. Components are re-usable, so we can make as many as we want:
jsx
function BlogPost() {
  return (
    <div>
      <BlogContent articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration." />
      <Comment />
      <Comment />
      <Comment />
    </div>
  );
}
then pass content data down to them:
jsx
function BlogPost() {
  return (
    <div>
      <BlogContent articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration." />
      <Comment commentText="I agree with this statement. - Angela Merkel" />
      <Comment commentText="A universal truth. - Noam Chomsky" />
      <Comment commentText="Truth is singular. Its ‘versions’ are mistruths. - Sonmi-451" />
    </div>
  );
}
We are passing information from a parent component to many child components. Specifically, we are doing this by creating a prop called `commentText` to pass to each `Comment` component, which is then accessible in each instance of `Comment` as `props.commentText`.

Rendered HTML:
`html
<div>
  <div>Dear Reader: Bjarne Stroustrup has the perfect lecture oration.</div>
  <div>I agree with this statement. - Angela Merkel</div>
  <div>A universal truth. - Noam Chomsky</div>
  <div>Truth is singular. Its ‘versions’ are mistruths - Sonmi-451</div>
</div>

Another example of conditional rendering
__________________________________
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}

create a Greeting component that displays either of these components depending on whether a user is logged in:
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

const root = ReactDOM.createRoot(document.getElementById('root')); 
// Try changing to isLoggedIn={true}:
root.render(<Greeting isLoggedIn={false} />);

Components
- are modular, reusable, and enable a 'templating' functionality
- help us organize our user interface's _logic_ and _presentation_
- enable us to think about each piece in isolation, and apply structure to
  complex programs

Props:
- are passed from a _parent component_ to a _child component_
- can be accessed in the _child components_ via an _object_ that is passed into
  our component function as an argument
- can hold any kind of data (strings, numbers, booleans, objects, even
  functions!)

##Props Destructuring and Default values
  Props reminder - 
  Props allow us to pass values into our components and these values can be anything: strings, objects, arrays, functions, etc.
  Props give us the abilty to make components more dynamic and reusable.
  
comparison of a component with hardcoded, static data against a component using props to make it more dynamic:

###static and hardcoded
jsx
function MovieCard() {
  return (
    <div className="movie-card">
      <img
        src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTn1OTYGz2GDC1XjA9tirh_1Rd571yE5UFIYsmZp4nACMd7CCHM"
        alt="Mad Max: Fury Road"
      />
      <h2>Mad Max: Fury Road</h2>
      <small>Genres: Action, Adventure, Science Fiction, Thriller</small>
    </div>
  );
}

###passing in props
Say we want to be able to render a movie card for a different movie. You do this by writing our components so they make use of props, which are passed from the parent.

To pass props to a component, you add them as attributes when you render the component, just like adding attributes to an HTML element:
jsx
const movieTitle = "Mad Max"
<MovieCard title={movieTitle} />
The value of the prop is enclosed in JSX curly braces. This value can be anything: a variable, inline values, functions, etc. If your value is a hardcoded string, you enclose it in double quotes.
jsx
<MovieCard title="Mad Max" />

###update component to make it dynamic using props:
jsx
parent component
function App() {
  const title = "Mad Max";
  const posterURL =
    "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTn1OTYGz2GDC1XjA9tirh_1Rd571yE5UFIYsmZp4nACMd7CCHM";
  const genresArr = ["Action", "Adventure", "Science Fiction", "Thriller"];

  return (
    <div className="App">
      {/* passing down props from the parent component */}
      <MovieCard title={title} posterSrc={posterURL} genres={genresArr} />
    </div>
  );
}

child component
function MovieCard(props) {
  return (
    <div className="movie-card">
      <img src={props.posterSrc} alt={props.title} />
      <h2>{props.title}</h2>
      <small>{props.genres.join(", ")}</small>
    </div>
  );
}

###Destructuring Props
React functions will only ever get called with one argument, which is the props object. Destructuring, a JavaScript feature, can make components cleaner.
jsx
function MovieCard({ title, posterSrc, genres }) {
  return (
    <div className="movie-card">
      <img src={posterSrc} alt={title} />
      <h2>{title}</h2>
      <small>{genres.join(", ")}</small>
    </div>
  );
}
in the above example, we're destructuring the 'props' object in the parameter in this function, which will have 'title', 'posterSrc' and 'genres' as keys.

Destructuring takes the keys from the props object and creates variables with the same names. That way, in our JSX, we don't have to use 'props.whatever' everywhere - the value associated with each key is stored in the corresponding variable, so it can be accessed directly.

Another benefit of destructuring props is that it makes it easier to tell what props a component expects to be passed down from its parent. Here are two versions of the same component:
jsx
// Without Destructuring
function MovieCard(props) {
  return (
    <div className="movie-card">
      <img src={props.posterSrc} alt={props.title} />
      <h2>{props.title}</h2>
      <small>{props.genres.join(", ")}</small>
    </div>
  );
}

// With Destructuring
function MovieCard({ title, posterSrc, genres }) {
  return (
    <div className="movie-card">
      <img src={posterSrc} alt={title} />
      <h2>{title}</h2>
      <small>{genres.join(", ")}</small>
    </div>
  );
}

without destructuring, we would have to find all the places wehre 'props' is referenced in the component to determine what props this component expects.

with destructuring, all we have to do is look at the function parameters and we can see exactly what props the component needs.

###Destructuring Nested Objects
jsx
function App() {
  const socialLinks = {
    github: "https://github.com/liza",
    linkedin: "https://www.linkedin.com/in/liza/",
  };

  return (
    <div>
      <SocialMedia links={socialLinks} />
    </div>
  );
}

function SocialMedia({ socialLinks }) {
  return (
    <div>
      <a href={socialLinks.github}>{socialLinks.github}</a>
      <a href={socialLinks.linkedin}>{socialLinks.linkedin}</a>
    </div>
  );
}

Since `socialLinks` is an object, we can also destructure it to make our JSX cleaner, either by destructuring in the body of the function:

```jsx
function SocialMedia({ socialLinks }) {
  const { github, linkedin } = socialLinks;

  return (
    <div>
      <a href={github}>{github}</a>
      <a href={linkedin}>{linkedin}</a>
    </div>
  );
}

...or by destructuring further in the parameters to our function:

jsx
function SocialMedia({ socialLinks: { github, linkedin } }) {
  return (
    <div>
      <a href={github}>{github}</a>
      <a href={linkedin}>{linkedin}</a>
    </div>
  );
}

###Default Values for Props
Say we are using our application to render a list of hundreds of movies, but the data set is not very reliable when it comes to movie poster URLs. To make sure the component doesn't render as a disaster when the data is incomplete, assign a default poster url when a bad one, or none at all, is provided. For instance, a Max Headroom poster URL is being used as a default placeholder below:
![max headroom poster](https://m.media-amazon.com/images/M/MV5BOTJjNzczMTUtNzc5MC00ODk0LWEwYjgtNzdiOTEyZmQxNzhmXkEyXkFqcGdeQXVyNzMzMjU5NDY@._V1_UY268_CR1,0,182,268_AL_.jpg)

Instead of passing in that default poster image in case we don't have one, we can tell our `MovieCard` component to use a **default value** if the `posterSrc` prop was not provided. To do this, we can add the default value to our destructured props:

```jsx
function MovieCard({
  title,
  genres,
  posterSrc = "https://m.media-amazon.com/images/M/MV5BOTJjNzczMTUtNzc5MC00ODk0LWEwYjgtNzdiOTEyZmQxNzhmXkEyXkFqcGdeQXVyNzMzMjU5NDY@._V1_UY268_CR1,0,182,268_AL_.jpg",
}) {
  return (
    <div className="movie-card">
      <img src={posterSrc} alt={title} />
      <h2>{title}</h2>
      <small>{genres.join(", ")}</small>
    </div>
  );
}

##Why Use Default Values
Because in React, we want components to encapsulate the functionality that they _can and should be responsible for_. The component that is responsible for rendering the movie information and poster should be handling the missing data. So the child, not the parent, should be responsible for managing the assignmnet of a default movie poster source value.

##Destructuring Conclusion
destructuring our components makes the returned JSX element easier to read, because we don't have to reference 'props.whatever' everywhere.

Destructuring makes it easier to tell what props a component expects. We just look at the destructured parameters instead of reading through the whole component and looking for references to the props object.

When we use destructuring, we can provide a **default value** for any prop keys we want, so that if the component doesn't receive those props from its parents, we can still render some default information.