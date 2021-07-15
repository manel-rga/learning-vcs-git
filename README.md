The Readme is structure in 5 sections:

- **CA1 Steps** : this section works like a step-by-step tutorial of the process followed in this CA(further details on the implementation can be found in the implementation section);
- **Requirements** : this section contains the requests made by the client;
- **Analysis**: a small analysis of the requests introduced in this CA;
- **Design**: details on the design of the solutions;
- **Implementation**: detailed displays of the chosen implementation(methods, classes, etc...);
- **original project info**: information provided in the original project README.

**CA1 Steps**

1.1 Setup project structure and Spring;
___
2.1 Create a new Tag:
```
   git tag v.1.2.0
```
2.2 Verify the creation of the Tag:
```
   git tag
```
___

3.1 Add files to staging:

- if adding all files use:
```
   git add .
```
- if adding specific files use:
```
   git add filename
```
3.2 Commit changes
```
   git commit -m "initial commit"
```
___
4.1 Link local and remote repository
```
   git remote add origin https://manel_rga@bitbucket.org/manel_rga/devops-20-21-1201770.git
```
4.2 Push files to remote repository
```
   git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```
___
5.1 Create a branch with "email-field" name:
```
   git branch email-field
```
5.2 Verify the creation of the branch:
```
   git branch
```
5.3 Change branches:
```
   git checkout email-field
```
___
6.1 Add Support for email field in Employee.java;

6.2 Add Support for email field in DatabaseLoader.java;

6.3 Add Support for email field in app.js;
___
7.1 Add unit tests for the creation of Employees and validation of Employees;
___
8.1 Ensure Server and Client parts are working as intended by running Spring and loading http://localhost:8080/;
___
9.1 Add all files and commit changes in branch email-field:
```
git add .
```
```
git commit -m "added email functionality and validation for employee creation and its attributes"
```
9.2 Created and pushed the branch to the remote depository:
```
git push --set-upstream origin email-field
```
or
```
git push -u origin email-field
```
___
10.1 Checkout Master:
```
git checkout master
```
10.2 Merge email-field branch into master:
```
git merge email-field
```
10.3 Create a new Tag:
```
   git tag v.1.3.0
```
10.4 Add, commit and push with tag:
```
git add .
```
```
git commit -m "merged email-field and made a few changes to README"
```
```
git push origin master v1.3.0
```
___
11.1 Create a branch with "fix-invalid-email" name:
```
   git branch fix-invalid-email
```
11.2 Verify the creation of the branch:
```
   git branch
```
11.3 Change branches:
```
   git checkout fix-invalid-email
```
11.4 Created and pushed the branch to the remote depository:
```
git push --set-upstream origin fix-invalid-email
```
___
12.1 Add validations for email field in Employee.java (using regex);
___
13.1 Add unit tests for the validation of emails;
___
14.1 Ensure Server and Client parts are working as intended;
___
15.1 Add and commit changes in branch email-field:
```
git add .
```
```
git commit -m "added proper email validation using regex"
```
15.2 Push changes to fix-invalid-email branch:
```
git push origin fix-invalid-email
```
15.3 Checkout Master:
```
git checkout master
```
15.4 Merge fix-invalid-email branch into master:
```
git merge fix-invalid-email
```
15.5 Create a new Tag:
```
   git tag v.1.3.1
```
15.6 Verify tag:
```
   git tag
```
15.7 Add, commit and push:
```
git add .
```
```
git commit -m "merged branch fix-invalid-email"
```
```
git push origin master v1.3.1
```
___
16.1 Create new tag to signalize completion:
```
   git tag ca1
```
16.2 Verify tag:
```
   git tag
```
16.3 Add, commit and push tag:
```
git add .
```
```
git commit -m "merged branch fix-invalid-email"
```
```
git push origin master ca1
```
___

**Requirements**

>*"You should develop new features in branches named after the feature. For instance, a branch named "email-field" to add a new email field to the application"*

>*"You should also add unit tests for testing the creation of Employees and the validation
of their attributes (for instance, no null/empty values)."*

>*"The server should only accept Employees with a valid email (e.g., an email must have the "@" sign)"*

Based on these notes, the requirements were assumed to be:

- Create email field for Employee.

- Validate and unit test attributes of Employee (including newly created email field).
  - Validation of email field: email must have the "@" sign.

___
**Analysis**

Given the requests, to implement the changed it is required that:

- Email field needs to be added in front and back-end so it is possible to display it.

- Employee attributes must be validated to ensure that only valid values are added.

___
**Design**

For the first request, a new email attribute, of the type String, should be added to the class Employee, in its constructor. This is done in a new, feature specific, branch. This attribute will store the email data of the employee.

Furthermore, employee attributes should be validated - the email field will be validated using Regex, while the other attributes can be just validated to ensure they have no null, empty or blank values.

Finally, the front-end will need to be updated to allow the display of the Employee information. The DatabaseLoader class as well as the app.js file will need to be updated for this purpose.

___
**Implementation**

- The Employee class attributes and Constructor were updated as follows:

```
public class Employee {

    private @Id
    @GeneratedValue
    Long id; // <2>
    private String firstName;
    private String lastName;
    private String description;
    private String jobTitle;
    private String email;

    public Employee() {
    
    }

    public Employee(String firstName, String lastName, String description, String jobTitle, String email) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.description = description;
        this.jobTitle = jobTitle;
        this.email = email;
        validateData();
    }

[...]

}
```

The validation of the data is separated into two elements: string Validation and email specific validation.

String Validation - since all attributes are Strings they can all be validated the same for null, empty or blank values.
If an invalid value is inputted an error message is thrown.
```
[...]
private void validateData() {
        this.firstName = validateString(this.firstName);
        this.lastName = validateString(this.lastName);
        this.description = validateString(this.description);
        this.jobTitle = validateString(this.jobTitle);
        checkEmailValidity();
    }

    private String validateString(String string) {
        if (string == null)
            throw new IllegalArgumentException ("Input is invalid or there hasn't been an input in field.");
        else if (string.isEmpty() || string.trim().length() == 0)
            throw new IllegalArgumentException ("Input is invalid or there hasn't been an input in field.");
        return string;
    }

```

---
---

**original project info**

# React and Spring Data Rest, Part 1

This projet contains part 1 (basic) of the tutorial react-and-spring-data-rest. See the original project at [react-and-spring-data-rest](https://github.com/spring-guides/tut-react-and-spring-data-rest/tree/master/basic).

The following contains the same documentation as the original project.

## Part 1 - Basic Features

[Original source folder](https://github.com/spring-guides/tut-react-and-spring-data-rest/tree/master)

Welcome, Spring community.

This section shows how to get a bare-bones Spring Data REST application up and running quickly. Then it shows how to build a simple UI on top of it by using Facebook's React.js toolset.

### Step 0 - Setting up Your Environment

Feel free to grab the code from this repository and follow along.

If you want to do it yourself, visit https://start.spring.io and pick the following dependencies:

* Rest Repositories
* Thymeleaf
* JPA
* H2

This demo uses Java 8, Maven Project, and the latest stable release of Spring Boot. It also uses React.js coded in [ES6](http://es6-features.org/). This will give you a clean, empty project. From there, you can add the various files shown explicitly in this section and/or borrow from the repository listed earlier.

**In the Beginning...**

In the beginning, there was data. And it was good. But then people wanted to access the data through various means. Over the years, people cobbled together lots of MVC controllers, many using Spring's powerful REST support. But doing over and over cost a lot of time.

Spring Data REST addresses how simple this problem can be if some assumptions are made:

* The developer uses a Spring Data project that supports the repository model.
* The system uses well accepted, industry standard protocols, such as HTTP verbs, standardized media types, and [IANA-approved link names](https://www.iana.org/assignments/link-relations/link-relations.xhtml).

**Declaring your domain**

Domain objects form the cornerstone of any Spring Data REST-based application. In this section, you will build an application to track the employees for a company. Kick that off by creating a data type, as follows:

./src/main/java/com/greglturnquist/payroll/Employee.java

`@Entity` is a JPA annotation that denotes the whole class for storage in a relational table.

`@Id` and `@GeneratedValue` are JPA annotations to note the primary key and that is generated automatically when needed.

This entity is used to track employee information -- in this case, their names and job descriptions.

NOTE: Spring Data REST is not confined to JPA. It supports many NoSQL data stores, though you will not see those in this tutorial. For more information, see [Accessing Neo4j Data with REST](https://spring.io/guides/gs/accessing-neo4j-data-rest/), [Accessing JPA Data with REST](https://spring.io/guides/gs/accessing-data-rest/), and [Accessing MongoDB Data with REST](https://spring.io/guides/gs/accessing-mongodb-data-rest/).

**Defining the Repository**

Another key piece of a Spring Data REST application is a corresponding repository definition, as follows:

./src/main/java/com/greglturnquist/payroll/EmployeeRepository.java

The repository extends Spring Data Commons' `CrudRepository` and plugs in the type of the domain object and its primary key

That is all that is needed! In fact, you need not even annotate interface if it is top-level and visible. If you use your IDE and open up `CrudRepository`, you will find a collection of pre-defined methods.

NOTE: You can define [your own repository](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.definition) if you wish. Spring Data REST supports that as well.

**Pre-loading the Demo**

To work with this application, you need to pre-load it with some data, as follows:

./src/main/java/com/greglturnquist/payroll/DatabaseLoader.java

This class is marked with Spring's `@Component` annotation so that it is automatically picked up by `@SpringBootApplication`.

It implements Spring Boot's `CommandLineRunner` so that it gets run after all the beans are created and registered.

It uses constructor injection and autowiring to get Spring Data's automatically created `EmployeeRepository`.

The `run()` method is invoked with command line arguments, loading up your data.

One of the biggest, most powerful features of Spring Data is its ability to write JPA queries for you. This not only cuts down on your development time, but it also reduces the risk of bugs and errors. Spring Data [looks at the name of methods](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.query-methods.details) in a repository class and figures out the operations you need, including saving, deleting, and finding.

That is how we can write an empty interface and inherit already built save, find, and delete operations.

**Adjusting the Root URI**

By default, Spring Data REST hosts a root collection of links at `/`. Because you will host a web UI on that path, you need to change the root URI, as follows:

./src/main/resources/application.properties

**Launching the Backend**

The last step needed to get a fully operational REST API off the ground is to write a `public static void main` mwethod by using Spring Boot, as follows:

./src/main/java/com/greglturnquist/payroll/

Assuming the previous class as well as your Maven build file were generated from https://start.spring.io, you can now launch it either by running that `main()` method inside your IDE or by typing `./mvnw spring-boot:run` on the command line. (`mvnw.bat` for Windows users).

NOTE: If you are not up-to-date on Spring Boot and how it works, you should watch one of [Josh Long's introductory presentations](https://www.youtube.com/watch?v=sbPSjI4tt10). Did it? Press on!

**Touring Your REST Service**

With the application running, you can check things out on the command line by using [cURL](https://curl.haxx.se/) (or any other tool you like). The following command (shown with its output) lists the links in the application:

```javascript
$ curl localhost:8080/api
{
  "_links" : {
    "employees" : {
      "href" : "http://localhost:8080/api/employees"
    },
    "profile" : {
      "href" : "http://localhost:8080/api/profile"
    }
  }
}
```

When you ping the root node, you get back a collection of links wrapped in a [HAL-formatted JSON document](http://stateless.co/hal_specification.html).

* `_links` is the collection of available links.
* `employees` points to an aggregate root for the employee objects defined by the `EmployeeRepository` interface.
* `profile` is an IANA-standard relation and points to discoverable metadata about the entire service. We explore this in a later section.

You can further dig into this service by navigating the `employees` link. The following command (shown with its output) does so:

```javascript
$ curl localhost:8080/api/employees
{
  "_embedded" : {
    "employees" : [ {
      "firstName" : "Frodo",
      "lastName" : "Baggins",
      "description" : "ring bearer",
      "_links" : {
        "self" : {
          "href" : "http://localhost:8080/api/employees/1"
        }
      }
    } ]
  }
}
```

At this stage, you are viewing the entire collection of employees.

Along with the data you pre-loaded earlier, a `_links` attribute with a `self` link is included. This is the canonical link for that particular employee. What is canonical? It means "`free of context`". For example, the same user could be fetched through `/api/orders/1/processor`, in which the employee is associated with processing a particular order. Here, there is no relationship to other entities.

IMPORTANT: Links are a critical facet of REST. They provide the power to navigate to related items. It makes it possible for other parties to navigate around your API without having to rewrite things every time there is a change. Updates in the client is a common problem when the clients hard-code paths to resources. Restructuring resources can cause big upheavals in code. If links are used and the navigation route is maintained, it becomes easy and flexible to make such adjustments.

You can decide to view that one employee if you wish. The following command (shown with its output) does so:

```javascript
$ curl localhost:8080/api/employees/1
{
  "firstName" : "Frodo",
  "lastName" : "Baggins",
  "description" : "ring bearer",
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/api/employees/1"
    }
  }
}
```

Little has changed here, except that there is no need for the `_embedded` wrapper since there is only the domain object.

That is all well and good, but you are probably itching to create some new entries. The following command (shown with its output) does so:

```javascript
$ curl -X POST localhost:8080/api/employees -d "{\"firstName\": \"Bilbo\", \"lastName\": \"Baggins\", \"description\": \"burglar\"}" -H "Content-Type:application/json"
{
  "firstName" : "Bilbo",
  "lastName" : "Baggins",
  "description" : "burglar",
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/api/employees/2"
    }
  }
}
```

You can also `PUT`, `PATCH`, and `DELETE`, as shown in [this related guide](https://spring.io/guides/gs/accessing-data-rest/). For now, though, we will move on to building a slick UI.

**Setting up a Custom UI Controller**

Spring Boot makes it super simple to stand up a custom web page. First, you need a Spring MVC controller, as follows:

./src/main/java/com/greglturnquist/payroll/HomeController.java

`@Controller` marks this class as a Spring MVC controller.

`@RequestMapping` flags the `index()` method to support the `/` route.

It returns `index` as the name of the template, which Spring Boot's autoconfigured view resolver will map to `src/main/resources/templates/index.html`.

**Defining an HTML template**

You are using Thymeleaf, although you will not really use many of its features. To get started you need an index page, as follows:

./src/main/resources/templates/index.html

The key part in this template is the `<div id="react"></div>` component in the middle. It is where you will direct React to plug in the rendered output.

You may also wonder where that `bundle.js` file came from. The way it is built is shown in the next section.

IMPORTANT: This tutorial does not show `main.css`, but you can see it linked up above. When it comes to CSS, Spring Boot will automatically serve anything found in `src/main/resources/static`. Put your own `main.css` file there. It is not shown in the tutorial, since our focus is on React and Spring Data REST, not CSS.

**Loading JavaScript Modules**

This section contains the barebones information to get the JavaScript bits off the ground. While you _can_ install all of JavaScripts command line tools, you need not do so -- at least, not yet. Instead, all you need to do is add the `frontend-maven-plugin` to your `pom.xml` build file.

This little plugin perform multiple steps:

* The `install-node-and-npm` command will install node.js and its package management tool, `npm`, into the `target` folder. (This ensures the binaries are NOT pulled under source control and can be cleaned out with `clean`).
* The `npm` command will execute the npm binary with the provided argument (`install`). This installs the modules defined in `package.json`.
* The `webpack` command will execute webpack binary, which compiles all the JavaScript code based on `webpack.config.js`.

These steps are run in sequence, essentially installing node.js, downloading JavaScript modules, and building the JS bits.

What modules are installed? JavaScript developers typically use `npm` to build up a `package.json` file, such as the following:

./package.json

Key dependencies include:

* react.js: The toolkit used by this tutorial
* rest.js: CujoJS toolkit used to make REST calls
* webpack: A toolkit used to compile JavaScript components into a single, loadable bundle
* babel: To write your JavaScript code using ES6 and compile it into ES5 to run in the browser

To build the JavaScript code you'll use later, you need to define a build file for [webpack](https://webpack.github.io/), as follows:

./webpack.config.js

This webpack configuration file:

* Defines the *entry point* as `./src/main/js/app.js`. In essence, `app.js` (a module you will write shortly) is the proverbial `public static void main()` of our JavaScript application. `webpack` must know this in order to know _what_ to launch when the final bundle is loaded by the browser.
* Creates *sourcemaps* so that, when you are debugging JS code in the browser, you can link back to original source code.
* Compile ALL of the JavaScript bits into `./src/main/resources/static/built/bundle.js`, which is a JavaScript equivalent to a Spring Boot uber JAR. All your custom code AND the modules pulled in by the `require()` calls are stuffed into this file.
* It hooks into the babel engine, using both `es2015` and `react` presets, in order to compile ES6 React code into a format able to be run in any standard browser.

For more details on how each of these JavaScript tools operates, please read their corresponding reference docs.

NOTE: Want to see your JavaScript changes automatically? Run `npm run-script watch` to put webpack into watch mode. It will regenerate `bundle.js` as you edit the source.

With all that in place, you can focus on the React bits, which are fetched after the DOM is loaded. It is broken down into parts, as follows:

Since you are using webpack to assemble things, go ahead and fetch the modules you need:

./src/main/js/app.js

`React` is one of the main libraries from Facebook used to build this app.

`client` is custom code that configures rest.js to include support for HAL, URI Templates, and other things. It also sets the default `Accept` request header to `application/hal+json`. You can [read the code here](https://github.com/spring-guides/tut-react-and-spring-data-rest/blob/master/basic/src/main/js/client.js).

IMPORTANT: The code for `client` is not shown because what you use to make REST calls is not important. Feel free to check the source, but the point is, you can plugin Restangular (or anything you like), and the concepts still apply.

**Diving into React**

React is based on defining components. Often, one component can hold multiple instances of another in a parent-child relationship. This concept can extend to several layers.

To start things off, it is very handy to have a top level container for all components. (This will become more evident as you expand upon the code throughout this series.) Right now, you only have the employee list. But you might need some other related components later on, so start with the following:

./src/main/js/app.js - App component

`class App extends React.Component{...}` is the method that creates a React component.

`componentDidMount` is the API invoked after React renders a component in the DOM.

`render` is the API that "`draws`" the component on the screen.

NOTE: In React, uppercase is the convention for naming components.

In the `App` component, an array of employees is fetched from the Spring Data REST backend and stored in this component's `state` data.

**NOTE**
React components have two types of data: *state* and *properties*.

*State* is data that the component is expected to handle itself. It is also data that can fluctuate and change. To read the state, you use `this.state`. To update it, you use `this.setState()`. Every time `this.setState()` is called, React updates the state, calculates a diff between the previous state and the new state, and injects a set of changes to the DOM on the page. This results in fast and efficient updates to your UI.

The common convention is to initialize state with all your attributes empty in the constructor. Then you look up data from the server by using `componentDidMount` and populating your attributes. From there on, updates can be driven by user action or other events.

*Properties* encompass data that is passed into the component. Properties do NOT change but are instead fixed values. To set them, you assign them to attributes when creating a new component, as you will soon see.


WARNING: JavaScript does not lock down data structures as other languages do. You can try to subvert properties by assigning values, but this does not work with React's differential engine and should be avoided.

In this code, the function loads data through `client`, a [Promise-compliant](https://promisesaplus.com/) instance of rest.js. When it is done retrieving from `/api/employees`, it then invokes the function inside `done()` and sets the state based on its HAL document (`response.entity._embedded.employees`). See the structure of `curl /api/employees` <<Touring your REST service,earlier>> and see how it maps onto this structure.

When the state is updated, the `render()` function is invoked by the framework. The employee state data is included in the creation of the `<EmployeeList />` React component as an input parameter.

The following listing shows the definition for an `EmployeeList`:

./src/main/js/app.js - EmployeeList component

Using JavaScript's map function, `this.props.employees` is transformed from an array of employee records into an array of `<Element />` React components (which you will see a little later).

Consider the following listing:

```javascript
<Employee key={employee._links.self.href} data={employee} />
```

The preceding listing creates a new React component (note the uppercase format) with two properties: *key* and *data*. These are supplied with values from `employee._links.self.href` and `employee`.

IMPORTANT: Whenever you work with Spring Data REST, the `self` link is the key for a given resource. React needs a unique identifier for child nodes, and `_links.self.href` is perfect.

Finally, you return an HTML table wrapped around the array of `employees` built with mapping, as follows:

```javascript
<table>
    <tr>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Description</th>
    </tr>
    {employees}
</table>
```

This simple layout of state, properties, and HTML shows how React lets you declaratively create a simple and easy-to-understand component.

**NOTE**

Does this code contain both HTML _and_ JavaScript? Yes, this is [JSX](https://facebook.github.io/jsx/). There is no requirement to use it. React can be written using pure JavaScript, but the JSX syntax is quite terse. Thanks to rapid work on the Babel.js, the transpiler provides both JSX and ES6 support all at once.

JSX also includes bits and pieces of [ES6](http://es6-features.org/#Constants). The one used in this code is the [arrow function](http://es6-features.org/#ExpressionBodies). It avoids creating a nested `function()` with its own scoped `this` and avoids needing a [`self` variable](https://stackoverflow.com/a/962040/28214).

Worried about mixing logic with your structure? React's APIs encourage nice, declarative structure combined with state and properties. Instead of mixing a bunch of unrelated JavaScript and HTML, React encourages building simple components with small bits of related state and properties that work well together. It lets you look at a single component and understand the design. Then they are easy to combine together for bigger structures.


Next, you need to actually define what an `<Employee />` is, as follows:

./src/main/js/app.js - Employee component

This component is very simple. It has a single HTML table row wrapped around the employee's three properties. The property itself is `this.props.employee`. Notice how passing in a JavaScript object makes it easy to pass along data fetched from the server.

Because this component does not manage any state nor deal with user input, there is nothing else to do. This might tempt you to cram it into the `<EmployeeList />` up above. Do not do it! Splitting your app up into small components that each do one job will make it easier to build up functionality in the future.

The last step is to render the whole thing, as follows:

./src/main/js/app.js - rendering code

`React.render()` accepts two arguments: a React component you defined as well as a DOM node to inject it into. Remember how you saw the `<div id="react"></div>` item earlier from the HTML page? This is where it gets picked up and plugged in.

With all this in place, re-run the application (`./mvnw spring-boot:run`) and visit http://localhost:8080. The following image shows the updated application:

![](https://github.com/spring-guides/tut-react-and-spring-data-rest/raw/master/basic/images/basic-1.png)

You can see the initial employee loaded up by the system.

Remember using cURL to create new entries? Do that again with the following command:

```javascript
curl -X POST localhost:8080/api/employees -d "{\"firstName\": \"Bilbo\", \"lastName\": \"Baggins\", \"description\": \"burglar\"}" -H "Content-Type:application/json"
```

Refresh the browser, and you should see the new entry:

![](https://github.com/spring-guides/tut-react-and-spring-data-rest/raw/master/basic/images/basic-2.png)

Now you can see both of them listed on the web site.

**Review**

In this section:

* You defined a domain object and a corresponding repository.
* You let Spring Data REST export it with full-blown hypermedia controls.
* You created two simple React components in a parent-child relationship.
* You fetched server data and rendered them in as a simple, static HTML structure.

Issues?

* The web page was not dynamic. You had to refresh the browser to fetch new records.
* The web page did not use any hypermedia controls or metadata. Instead, it was hardcoded to fetch data from `/api/employees`.
* It is read only. While you can alter records using cURL, the web page offers no interactivity.
