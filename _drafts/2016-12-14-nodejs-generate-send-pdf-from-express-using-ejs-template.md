---
layout: post
title: "[NodeJs] generate send pdf from express using ejs template"
description: ""
category: memo
tags: []
---
{% include JB/setup %}


# install

```bash
$ npm install --save ejs
```

# template

```ejs
<html>
<head>
  <title><%= title %></title>
</head>
<body>
  You have a new mission <%= ninja.name %>
  <table>
    <thead>
      <tr>
        <th>target</th>
        <th>action</th>
      </tr>
    </thead>
    <tbody>

      <% for(let i=0; i < mission.target.length; i++) { %>
        <tr>
          <td><%= mission.target[i].name %></td>
          <td><%= mission.target[i].action %></td>
        </tr>
      <% } %>

    </tbody>
  </table>
</body>
</html>
```

# from ejs file to html string

```javascript
"use strict";
import ejs from "ejs";

/**
 * @param {Object} options
 * @param {String} options.category
 * @param {String} options.template
 * @param {Object} options.data
 *
 * @return {Promise.<String, Error>}
 */
let parseTemplateToString = (options) => {
  let {category, template, data} = options;

  return new Promise(
    (resolve, reject) => {
      let filePath = `${__dirname}/../templates/${category}/${template}.ejs`;
      let renderingOptions = {
        client: true,
        rmWhitespace: true
      };
      ejs.renderFile(
        filePath,
        data,
        renderingOptions,
        (err, str) => {
          if(err) return reject(err);
          return resolve(str);
        }
      )
    }
  );
}

export default parseTemplateToString;
```

# from string to pdf file

```bash
$ npm install --save phantom-html-to-pdf phantomjs-prebuilt
```

```javascript
"use strict";
import fs from "fs";
import renderTemplateToString from "../templates"
const converter = require("phantom-html-to-pdf")({
  numberOfWorker: 2,
  timeout: 5000,
  tmpDir: "/tmp",
  phantomPath: require("phantomjs-prebuilt").path,
  strategy: "dedicated-process"
});

/**
 * @param {Object} ninja - data for the template
 * @returns {Promise.<String, Error>}
 */
const generateReport = (ninja) => {
  return renderTemplateToString(
    {
      category: "ninja",
      template: "newMission",
      data: {
        ninja
      }
    }
  )
    .then(
      template => {
        return new Promise(
          (resolve, reject) => {
            converter(
              {
                html: template
              },
              (err, pdf) => {
                if(err) return reject(err);
                return resolve(pdf.stream.path)
              }
            )
          }
        )
      }
    )

};

export default generateReport;

```

# Express endpoint

```javascript
// other imports
import generatePdfService from "../services/generateReport"
// other express and other stuff
app.get(
  "/report/:ninjaId",
  (request, response) => {
    findNinja(request.params.ninjaId)
      .then(
        ninja => {
          return generatePdfService(ninja);
        }
      )
      .then(
        path => {
          response.setHeader("Content-disposition", "'inline; filename=report.pdf'");
          response.setHeader("Content-Type", "application/pdf");
          response.sendFile(path);

          /*
          the file is still there lying in the tmp directory....
          */
        }
      )
  }
);
// continue express and other stuff
```


# Documentation

## EJS templates

- https://www.npmjs.com/package/ejs

# PDF generation

- https://www.npmjs.com/package/phantom-html-to-pdf
- https://github.com/pofider/phantom-html-to-pdf
- https://www.npmjs.com/package/phantomjs-prebuilt

# NodeJs

- http://stackoverflow.com/questions/8817423/node-dirname-not-defined
