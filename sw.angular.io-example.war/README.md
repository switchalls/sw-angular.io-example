# angular.io tutorial (webapp)

POM plugin setup based on
[dzone.com](https://dzone.com/articles/building-a-web-app-using-spring-boot-angular-6-and)

Change symbolic link `src/main/web` to select required application.

## Default application (`np-app`)

Install [angular-cli](https://cli.angular.io/)

```bash
$ brew install angular-cli
```

Create *new* angular project

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

Changed `name` in `src/package.json`

Replaced all occurrences of `np-app` in `src/angular.json`, eg.

```json
  "projects": {
    "np-app": {
      "projectType": "application",
      ...
          "options": {
            "browserTarget": "np-app:build"
          },
```

Changed `title` in `src/index.html`

Added import for `Material Icons` in `src/index.html`, eg.

```html
  <link
    href="https://fonts.googleapis.com/icon?family=Material+Icons"
    rel="stylesheet"
  />
</head>
```

## Adding new components

Create component files, eg.

* app/product-alerts/product-alerts.component.css
* app/product-alerts/product-alerts.component.html
* app/product-alerts/product-alerts.component.ts


Add new component to `app.module.ts`, eg.

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
