#Stylesheet guidelines

Currently we are using in almost all projects [SASS](http://sass-lang.com/). Therefor we have style guidelines which are defined by SCSS-Lint.

##SCSS-Lint

Please read the [Documentation](https://github.com/causes/scss-lint) to know what exactely SCSS-LINT is and how it works.

###Integrating SCSS-Lint in your development environment

The scss-lint-config.yml defines the yetu style guidelines and should be placed in the root folder of the project.   
[How-to-integrate in IntelliJ, Webstorm & Co](https://github.com/idok/scss-lint-plugin)   
[How-to-integrate in Sublime](https://sublime.wbond.net/packages/SublimeLinter-contrib-scss-lint)

It would be great, if we try to integrate a grunt or gulp task to check the style in all projects. As a first step it 
should be only added as a subtask to the dev tasks.  
When all files are free of warnings, it can be added to the build tasks for server as well.  
The following plugins should be used for that:  
[Grunt-SCSS-Lint Plugin](https://www.npmjs.org/package/grunt-scss-lint)  
[Gulp-SCSS-Lint Plugin](https://www.npmjs.org/package/gulp-scss-lint) 

##Shifter

One guideline in the SCSS-File is to have alphabetically sorted list of class-properties.
Shifter is a plugin for IntelliJ, Webstorm&Co to sort many lines per alphabet.

