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
