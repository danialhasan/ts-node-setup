# Typescript and Node integration setup

This is how to setup a new project with typescript, nodejs, and express.
In the future I plan to use an alias function in the terminal itself to automate all of this stuff. All it will ask me for is:

1. Name of project root directory (main project name)
2. Git repo? (Y/N)
3. Tailwind integration? (Y/N)

**_Terminal Commands_**
<br>
_Make sure you're in your project directory before running the following terminal commands! The alias is ts_node_newproject_

### Typescript + Node(with types) + Express(with types)

```
npm init -y; npm i -D typescript ts-node nodemon @types/node @types/express; npm i express; tsc --init; mkdir src && cd src && touch app.ts && cd .. && code .;

```

### Typescript + Node(with types) + Express(with types) + DotEnv + Tailwind (With PostCSS and Autoprefixer)

```
npm init -y; npm i -D typescript ts-node nodemon @types/node @types/express dotenv tailwindcss@latest postcss@latest autoprefixer@latest; npm i express; tsc --init; mkdir src && cd src && touch app.ts && cd .. && code .;

npm init -y; npm i -D typescript ts-node nodemon @types/node @types/express dotenv tailwindcss@latest postcss@latest autoprefixer@latest;print "Dev Dependencies Installed✅"; npm i express; print "Regular Dependencies Installed✅"; tsc --init; mkdir src && cd src && touch app.ts && cd .. && mkdir config && cd config && touch .env && cd .. && mkdir public && cd public && mkdir assets styles scripts && cd styles && touch stylesheet.css && ../.. && npx tailwindcss init && code . && code tsconfig.json package.json; print "\n\nSetup Complete ✅\n\nNext Steps: \n1. Set up Scripts\n2. Set up tsconfig.json\n3. Set up tailwindCSS by adding @tailwind code to public/styles/stylesheets and editing config file. Then, call npm build:css script.\n\n"

```

<hr>
<br><br>

### Typescript + Node(with types) + Express(with types) + DotEnv + Tailwind (With PostCSS and Autoprefixer) + EJS + Express EJS Layouts

```
npm init -y;
npm i -D typescript ts-node nodemon @types/node @types/express dotenv tailwindcss@latest postcss@latest autoprefixer@latest;
print "Dev Dependencies Installed✅";
npm i express ejs express-ejs-layouts;
print "Regular Dependencies Installed✅";
tsc --init;
mkdir src && cd src && mkdir routes && touch app.ts &&
cd .. && mkdir views config && cd config && touch .env &&
cd .. && mkdir public && cd public && mkdir assets styles scripts &&
cd .. && cd views && touch layout.ejs index.ejs &&
cd ../src/routes && touch index.ts && cd ../.. &&
npx tailwindcss init && code . && code tsconfig.json package.json;
print "\n\nSetup Complete ✅\n\nNext Steps: \n1. Set up Scripts\n2. Set up tsconfig.json and tailwind.config.json\n\n" &&
cd public/styles; mkdir dist src; cd src; touch stylesheet.css; cd ../../..

```

Scripts for package.json.
**_Ideally we'd want to automate this in the terminal commands as well. Maybe parse package.json for "test" script and replace that with the following scripts?_**

```
"start":"node dist/app.js",
"dev":"nodemon src/app.ts",
"build":"tsc -p .",
"build:css":"npx tailwindcss-cli@latest build ./public/styles/tailwind.css -o ./public/styles/stylesheet.css"

```

1. Go to tsconfig.json
2. Go to "target" and change to ES6 or ES2020.
3. Go to outDir and change it to "dist".
4. Go to rootDir and change it to "src".
5. Uncomment moduleResolution to node.
6. You can now type ts code in src/app.ts and then the terminal will be watching your code. It will point out any errors as you make them.
7. Go to Tailwind config file.
8. Put views in purge array. Comment them out until you push to production.
9. In ./public/styles/src/stylesheet.css, paste the following code:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

10. Set up app.ts with the following code, then paste in layout.ejs.

```typescript
import express, { Application, Request, Response } from "express";
import path from "path";
require("dotenv").config();

const app: Application = express();
var expressLayouts = require("express-ejs-layouts");

const port = process.env.PORT || 5000;

//templating middleware
app.set("view engine", "ejs");
app.use(expressLayouts);

app.use(express.static("public"));
//routes
app.use("/", require("./routes/index.ts"));

// app.get('/', (req:Request, res:Response)=>res.send("Hello!"));

app.listen(port, () => console.log(`Listening on port ${port}`));
```

This will set your app up with:

- Express
- Dotenv
- EJS
- Express Layouts
- Public (for serving static files)
- Routes (Initial route to index.ts)


# todo: put all actionable, copy-paste-able text in the alias, and display with a print command
