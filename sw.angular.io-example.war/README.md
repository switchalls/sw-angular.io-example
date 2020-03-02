# angular.io tutorial (webapp)

POM based on `dzone.com`
[article](https://dzone.com/articles/building-a-web-app-using-spring-boot-angular-6-and)

Change symbolic link `src/main/web` to select required application.

## Angular projects

Angular projects consist of:
* project files, eg. `package.json`
* application files, eg. `src/app`

*NB.* Some `src` files are are also project related (eg. `polyfills.ts`)

New projects should *always* be created using `ng new`

## Live Development Server

Applications can run using the `ng serve`, eg.

```bash
$ cd sw.angular.io-example.war/src/main/web
$ ng serve

chunk {main} main.js, main.js.map (main) 34 kB [initial] [rendered]
chunk {polyfills} polyfills.js, polyfills.js.map (polyfills) 140 kB [initial] [rendered]
chunk {runtime} runtime.js, runtime.js.map (runtime) 6.15 kB [entry] [rendered]
chunk {styles} styles.js, styles.js.map (styles) 16.7 kB [initial] [rendered]
chunk {vendor} vendor.js, vendor.js.map (vendor) 3.3 MB [initial] [rendered]
Date: 2020-03-02T17:51:59.548Z - Hash: c5727d85e245be389cfc - Time: 4916ms
** Angular Live Development Server is listening on localhost:4200, open your browser on http://localhost:4200/ **
: Compiled successfully.
```

The server will automatically rebuilt the application whenever changes are made.

## Default application (`np-app`)

Install [angular-cli](https://cli.angular.io/), eg.

```bash
$ brew install angular-cli
```

Create a *new* angular project, eg.

```bash
$ cd sw.angular.io-example.war/src/main
$ ng new -skip-git np-app
? Would you like to add Angular routing? No
? Which stylesheet format would you like to use? CSS
```

Change `npm` output in `angular.json`

```json
"builder": "@angular-devkit/build-angular:browser",
"options": {
    "outputPath": "../../../target/dist",
```

## angular.io-example

Cloned `src/main/np-app`

Replaced `src/app` from [angular.io](https://angular.io/start)

Replaced `src/styles.css` from [angular.io](https://angular.io/start)

Changed `title` in `src/index.html`

Added import for `Material Icons` in `src/index.html`, eg.

```html
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
</head>
```

Changed `name` in `src/package.json`

Replaced all occurrences of string "np-app" in `src/angular.json`, eg.

```json
  "projects": {
    "np-app": {
      "projectType": "application",
      ...
          "options": {
            "browserTarget": "np-app:build"
          },
```

## Adding new components

Create component files, eg.

* app/product-alerts/product-alerts.component.css
* app/product-alerts/product-alerts.component.html
* app/product-alerts/product-alerts.component.ts


Add component declaration to `app.module.ts`, eg.

```typescript
import { ProductAlertsComponent } from './product-alerts/product-alerts.component';

@NgModule({
  declarations: [
    ...
    ProductAlertsComponent
  ],
```

*Warning -* The application will fail to display the home page if any of the plumbing 
is done incorrectly.

