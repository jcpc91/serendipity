# Serendipity Developer Documentation

Good tools make application development better and easier.

The [Angular CLI](https://cli.angular.io/) is a command line tool that you can use to create the scaffolding for a new project, add files to a project and perform a variety of common development tasks.

## Quick Start

The goal of this guide is to help you build and run Serendipity using the Angular CLI.

### Step 1. Set up the Development Environment 

You need to set up your development environment before you can do anything.

Open a terminal window and install [Node.js (and npm)](https://nodejs.org/en/download/) and [git](https://git-scm.com/) if they are not already on your machine.

> Verify that you are running at least Node.js version 8.x or greater and npm version 5.x or greater by running node -v and npm -v in a terminal/console window. Older versions produce errors, but newer versions are fine.

Then install the Angular CLI globally:

```
npm install -g @angular/cli
```

### Step 2. Clone the project 

Change the current working directory to the location where you want the cloned directory to be:

```
cd ~/workspaces
```

Clone the project by running the following command:

```
git clone https://github.com/Robinyo/serendipity
```

### Step 3: Launch Flowable 

The easiest way to get started with [Flowable](https://www.flowable.org/index.html) is to use a Docker image, for example:

```
docker run --name flowable -p 8080:8080 flowable/all-in-one
```

or

```
docker start --interactive flowable
```

To list all running containers:

```
docker container ls
```

You can stop a container using the following command:

```
docker container stop [name]
```

For example:

```
docker container stop flowable
docker container stop flowable-rest
```

During **development** we can use the [proxying](https://github.com/angular/angular-cli/blob/master/docs/documentation/stories/proxy.md) support in webpack's dev server to highjack certain URIs and send them to a backend server:

```
ng serve --proxy-config=proxy.conf.json
```

proxy.conf.json:

```
{
  "/flowable-task": {
    "target": "http://localhost:8080",
    "secure": false,
    "logLevel": "debug"
  }
}
```

### Step 4: Serve the application 

Go to the project directory, install the project's dependencies and launch the server:

```
cd serendipity
npm install
ng build utils && ng build auth && ng build flowable && ng build serendipity-components && ng build dynamic-forms && ng build sales
ng serve --proxy-config=proxy.conf.json --open
```

The ng serve command launches the server, watches your files, and rebuilds the app as you make changes to those files.

Using the --open (or just -o) option will open your browser on `http://localhost:4200/`

## Build Management

### Aliases

Steps to add support for aliases update the "paths" array in the `compilerOptions` section of `tsconfig.json`:

```
  "paths": {
    "@app/*": [
      "src/app/*"
    ],
    "@env/*": [
      "src/environments/*"
    ],

    ...
    
  }
```

### Development

To build the project:

```
ng build utils && ng build auth && ng build flowable && ng build serendipity-components && ng build dynamic-forms && ng build sales
```
       
To launch the project:

```
ng serve --proxy-config=proxy.conf.json
```

Navigate to:

```
http://localhost:4200/
```

The app will automatically reload if you change any of the source files.

### Production

To update the project's version:

```
npm run version-update -- 1.0.0-beta.1
```

To build the project:

```
ng build utils && ng build auth && ng build flowable && ng build serendipity-components && ng build dynamic-forms && ng build sales
ng build --prod --source-map 
```

The build artifacts will be stored in the `dist/serendipity` directory. 

To launch the project using [http-server](https://github.com/indexzero/http-server):

```
http-server -p 8080 -c-1 dist/serendipity
```

**Note:** To reduce the possibility of conflicts and avoid serving stale content, test on a dedicated port and disable caching.

Navigate to:

```
http://127.0.0.1:8080
```

To launch the project using Firebase:

```
firebase serve
```
 
Navigate to:
 
```
http://localhost:5000
```

To deploy the project to Firebase Hosting:

```
firebase deploy
```

Navigate to:

```
https://serendipity-f7626.firebaseapp.com
```

### Code scaffolding

Run `ng generate component component-name` to generate a new component. 

You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

### Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

### Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

### Project Assets

You use the assets array inside the build target in `angular.json` to list files or folders you want to copy as-is when building your project:

```
"assets": [
  "src/assets",
  "src/favicon.ico",
  "src/manifest.json"
]
```

### Library Assets

ng-packagr does not copy 'assets' (the files and folders in the `assets/` directory) to the `dist/` directory.

You can workaround this issue by updating the assets array inside the build target in `angular.json`, for example:

```
"assets": [
  "src/assets",
  "src/favicon.ico",
  "src/manifest.json",
  {
    "glob": "**/*",
    "input": "projects/sales/src/assets",
    "output": "/assets"
  },
  {
    "glob": "**/*",
    "input": "node_modules/my-lib/assets",
    "output": "/assets"
  }
]
```

### Source Control

Check in:

```
git add .
git commit -m "Updated the README.md file"
git push -u origin master
```

Tag Format:

```
1.0.0-beta.1
```

To create a local tag on your current branch, run this:

```
git tag <tagname>
```

To push the local tags to GitHub:

```
git push origin --tags
```

or

```
git push origin <tag>
```

### WebStrom

To disable the 'Angular Language Service', go to WebStorm -> Preferences -> Languages & Frameworks -> TypeScript and clear the 'Angular Language Service' checkbox.

## Angular Resources

* Angular.io: [Quick Start Guide](https://angular.io/guide/quickstart)
* Angular.io: [Style Guide](https://angular.io/guide/styleguide)
* GitHub: [Angular, one framework for Mobile & Desktop](https://github.com/angular/angular)
* GitHub: [A curated list of awesome Angular resources](https://github.com/gdi2290/awesome-angular)
* GitHub: [Catalog of Angular 2+ Components & Libraries](https://github.com/brillout/awesome-angular-components)

## Angular CLI Resources

* GitHub: [Library support in the Angular CLI](https://github.com/angular/angular-cli/wiki/stories-create-library)
* Medium: [6 Best Practices & Pro Tips when using Angular CLI](https://medium.com/@tomastrajan/6-best-practices-pro-tips-for-angular-cli-better-developer-experience-7b328bc9db81)
* Medium: [Compiling css in new Angular 6 libraries](https://medium.com/@Dor3nz/compiling-css-in-new-angular-6-libraries-26f80274d8e5)
* GitHub: [Project Assets](https://github.com/angular/angular-cli/wiki/stories-asset-configuration)

## Material Design Resources

* Material.io: [Material Design, make beautiful products, faster](https://material.io/)
* GitHub: [Material Design for Angular](https://github.com/angular/material2)
* GitHub: [Covalent - The Teradata UI Platform built on Angular Material](https://teradata.github.io/covalent/#/docs)

## Angular Component Libraries

* GitHub: [flex-layout](https://github.com/angular/flex-layout)
* GitHub: [ngx-charts](https://github.com/swimlane/ngx-charts)

## Angular Form Libraries

* GitHub: [ng-dynamic-forms](https://github.com/udos86/ng-dynamic-forms)
* GitHub: [ngx-formly](https://github.com/formly-js/ngx-formly)
* GitHub: [angular-schema-form (AngularJS) - Generate forms from a JSON schema](https://github.com/json-schema-form/angular-schema-form)
* GitHub: [ngx-schema-form - HTML form generation based on JSON Schema](https://github.com/guillotinaweb/ngx-schema-form)
* GitHub: [angular2-json-schema-form - Angular 2 JSON Schema Form builder](https://github.com/dschnelldavis/angular2-json-schema-form)
* form.io: [form.io - A Form and Data Management Platform](https://www.form.io/)

## Angular i18N

* GitHub: [ngx-translate](https://github.com/ngx-translate/core)

## Additional Angular Component Libraries

* GitHub: [Angular in-memory Web API](https://github.com/angular/in-memory-web-api)
* GitHub: [json-server](https://github.com/typicode/json-server)
* GitHub: [Hotel - A simple process manager for developers](https://github.com/typicode/hotel)
* GitHub: [angular-split](https://github.com/bertrandg/angular-split/)

## CSS Grid Layout

* CSS Tricks: [A Complete Guide to CSS Grid Layout](https://css-tricks.com/snippets/css/complete-guide-grid/)
* Grid By Example: [CSS Grid Layout by Example](https://gridbyexample.com/learn/)

## Sample Data

* Wikipedia: [List of political parties in Australia](https://en.wikipedia.org/wiki/List_of_political_parties_in_Australia)
* Australian Parliament: [Mail Labels for Australian Senators](https://www.aph.gov.au/Senators_and_Members/Guidelines_for_Contacting_Senators_and_Members/Address_labels_and_CSV_files)
