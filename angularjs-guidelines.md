# AngularJS Style Guide

## Main Priorities

* Always keep "code user" in your mind
* Try to stay on Functional Programming way
* Keep structure and complexity controllable
* Keep things consistent
* Strive for functional decomposition (group by functionality)

## Components
	
1. Strive for reusable components.  
  ***Why***: *Components help keeping project structure modifiable.  
  They help control complexity.*
  
2. Use [browserify](http://browserify.org/) for component bundling.  
  ***Why***: *Browserify allows us create packages with local references for dependencies (without specifying long paths like: `../../../myTemplate.html`)*

3. Use **self-contained components** for functional decomposition.   
  Here is [a simple example](https://github.com/mr-mig/angular-experiments/tree/master/ng-browserify-stringify/user).  
  Module sctructure looks like that:

        
        /login
          /tests
            prjLoginService.spec.js
          prjLoginService.js
          prjLoginFormDirective.js
          prjLoginForm.html
          prjLoginForm.css
          PrjLoginDataFactory.js
          index.js // this file has angular-specific code and all requires
  ***Why***: *Independent components reduce the number of dependency links.  
  It helps to reason about the dependency graph.  
  Keeps things maintainable.  
  Components can be reused in another project.*


## Project structure

Strive for component-based project structure. Good example is:
```
/bower_components
/assets
  /img
/components
  /common
  /categories
  /app_details
  /app_list
  /user_list
```
***Why:*** *This structure helps to control the complexity and can be easily evolved.  
Easier to navigate the working tree.*  
***Note***: *A better structure is being developed.*

## Naming conventions

Use camelCase for all components names.

### Prefixes
1. If you are creating or refactoring **a reusable component**, which can be used in several projects - you **must** use `yetu` prefix.
2. If you are creating a **subproject**, you **must** use the project name prefix(e.g. `hsc` for homescreen)  
3. If you are creating a locally used component, you **may** omit the prefix.

Good:  
`yetuUser.js`  
`yetuUserDirective.js`  
`cwTile.js`  
Bad:  
`User.js`,  
`userDirective.js`  
`Tile.js`

***Why***: *We do not want to have name collisions.   
Angular have no named injectors, so we need to use prefixes for reusable things.*

### Suffixes

#### Directives

1. Do not use `directive` suffix in directive name.  
2. First letter in **lower case**

Good:  
`.directive('yetuSearch', ...);`  
Bad:  
`.directive('yetuSearchDirective', ...);`

***Why***: *We do not want to write `<yetu-search-directive>` in templates.*

#### Models

1. Use `Model` suffix in model name.
2. First letter in **upper case**.

Good:  
`.factory('YetuUserModel', ...);`  
Bad:  
`.factory('YetuUser', ...);`

***Why***: *Both directive and model are Domain Specific Words and can be written without suffix in general.  
We do not want to mix components together and be confused while searching for component.*

#### Services

1. Use **plural without suffix**  for naming funcitional services (namespaces): `yetuUsers`
2. Use **singular with postfix** for naming service object: `yetuUserService`
3. First letter in **lower case**

#### Factories

1. Factory is different from service only by it's intent: use it when you need to create something manually when factory is used.
2. Naming convention is the same as for services.
3. First letter in **upper case**: `YetuUsers`.

#### Filters

1. Use **verbs** for filter functions: `yetuLinearize`, `yetuFormatDate`
2. First letter in **lower case**

#### Controllers

1. User `Controller` suffix.
2. First letter in **upper case**: `YetuLoginController`

### Intention Segregation
1. Use `lowerCase` names for all *singletons* and *instances* (service, directive, template, style, filter).
2. Use `UpperCase` names for all things, that *will* or *need* to be created (factory, controller, model class).

```javascript  
YetuUserModel       // must be created (new YetuUserModel()) in code 
app                 // a singleton instance 
registrationService // a singleton instance, no need to create it in code 
ValidationService   // must be created in code
```

***Why***: *We want to show "code user" how he should use the component: whether it is a ready instance, or he have to instantiate it, or it will be freshly instantiated each time.*  

### File Names

1. Use camelCase for file names  
***Why***: *To be consistent with component name style.*
2. `File name` = `component name` + `suffix` (if component has no suffix) + `extension`  
***Why***: *We want to know what component is in the file from the first glance.  
Helps locate components fast.*
3. File names must be unique without regards to case, e.g. we cannot have `appDirective.js` and `AppDirective.js` simultaneously.
***Why***: *We do not want problems in Git and on Mac OS.*


```javascript
.directive('yetuUser', require('./yetuUserDirective.js'));
```
```javascript 
.factory('YetuUser', require('./YetuUserModel.js'));
```
```javascript
.service('yetuLoginService', require('./yetuLoginService.js'));
```

### References
To have a better understanding of what's going on, have a look at other good styleguides:

* [johnpapa/angularjs-styleguide](https://github.com/johnpapa/angularjs-styleguide)
* [gocardless/angularjs-style-guide](https://github.com/gocardless/angularjs-style-guide)
