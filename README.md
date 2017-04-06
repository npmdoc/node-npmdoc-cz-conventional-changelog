# api documentation for  [cz-conventional-changelog (v2.0.0)](https://github.com/commitizen/cz-conventional-changelog)  [![npm package](https://img.shields.io/npm/v/npmdoc-cz-conventional-changelog.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-cz-conventional-changelog) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-cz-conventional-changelog.svg)](https://travis-ci.org/npmdoc/node-npmdoc-cz-conventional-changelog)
#### Commitizen adapter following the conventional-changelog format.

[![NPM](https://nodei.co/npm/cz-conventional-changelog.png?downloads=true)](https://www.npmjs.com/package/cz-conventional-changelog)

[![apidoc](https://npmdoc.github.io/node-npmdoc-cz-conventional-changelog/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-cz-conventional-changelog_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-cz-conventional-changelog/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-cz-conventional-changelog/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-cz-conventional-changelog/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Jim Cummins",
        "email": "jimthedev@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/commitizen/cz-conventional-changelog/issues"
    },
    "czConfig": {
        "path": "./"
    },
    "dependencies": {
        "conventional-commit-types": "^2.0.0",
        "lodash.map": "^4.5.1",
        "longest": "^1.0.1",
        "pad-right": "^0.2.2",
        "right-pad": "^1.0.1",
        "word-wrap": "^1.0.3"
    },
    "description": "Commitizen adapter following the conventional-changelog format.",
    "devDependencies": {
        "commitizen": "2.9.6",
        "semantic-release": "^6.3.2"
    },
    "directories": {},
    "dist": {
        "shasum": "55a979afdfe95e7024879d2a0f5924630170b533",
        "tarball": "https://registry.npmjs.org/cz-conventional-changelog/-/cz-conventional-changelog-2.0.0.tgz"
    },
    "gitHead": "2d78e1d442cc18ea276e05e7ba8259615b3c3ddc",
    "homepage": "https://github.com/commitizen/cz-conventional-changelog",
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "commitizen-bot",
            "email": "kent+commitizen-bot@doddsfamily.us"
        },
        {
            "name": "jimthedev",
            "email": "jimthedev@gmail.com"
        },
        {
            "name": "kentcdodds",
            "email": "kent@doddsfamily.us"
        }
    ],
    "name": "cz-conventional-changelog",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/commitizen/cz-conventional-changelog.git"
    },
    "scripts": {
        "commit": "git-cz",
        "semantic-release": "semantic-release pre && npm publish && semantic-release post",
        "test": "echo 'Tests need to be setup!'"
    },
    "version": "2.0.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module cz-conventional-changelog](#apidoc.module.cz-conventional-changelog)
1.  [function <span class="apidocSignatureSpan">cz-conventional-changelog.</span>prompter (cz, commit)](#apidoc.element.cz-conventional-changelog.prompter)



# <a name="apidoc.module.cz-conventional-changelog"></a>[module cz-conventional-changelog](#apidoc.module.cz-conventional-changelog)

#### <a name="apidoc.element.cz-conventional-changelog.prompter"></a>[function <span class="apidocSignatureSpan">cz-conventional-changelog.</span>prompter (cz, commit)](#apidoc.element.cz-conventional-changelog.prompter)
- description and source-code
```javascript
prompter = function (cz, commit) {
  console.log('\nLine 1 will be cropped at 100 characters. All other lines will be wrapped after 100 characters.\n');

  // Let's ask some questions of the user
  // so that we can populate our commit
  // template.
  //
  // See inquirer.js docs for specifics.
  // You can also opt to use another input
  // collection library if you prefer.
  cz.prompt([
    {
      type: 'list',
      name: 'type',
      message: 'Select the type of change that you\'re committing:',
      choices: choices
    }, {
      type: 'input',
      name: 'scope',
      message: 'Denote the scope of this change ($location, $browser, $compile, etc.):\n'
    }, {
      type: 'input',
      name: 'subject',
      message: 'Write a short, imperative tense description of the change:\n'
    }, {
      type: 'input',
      name: 'body',
      message: 'Provide a longer description of the change:\n'
    }, {
      type: 'input',
      name: 'breaking',
      message: 'List any breaking changes:\n'
    }, {
      type: 'input',
      name: 'issues',
      message: 'List any issues closed by this change:\n'
    }
  ]).then(function(answers) {

    var maxLineWidth = 100;

    var wrapOptions = {
      trim: true,
      newline: '\n',
      indent:'',
      width: maxLineWidth
    };

    // parentheses are only needed when a scope is present
    var scope = answers.scope.trim();
    scope = scope ? '(' + answers.scope.trim() + ')' : '';

    // Hard limit this line
    var head = (answers.type + scope + ': ' + answers.subject.trim()).slice(0, maxLineWidth);

    // Wrap these lines at 100 characters
    var body = wrap(answers.body, wrapOptions);

    // Apply breaking change prefix, removing it if already present
    var breaking = answers.breaking.trim();
    breaking = breaking ? 'BREAKING CHANGE: ' + breaking.replace(/^BREAKING CHANGE: /, '') : '';
    breaking = wrap(breaking, wrapOptions);

    var issues = wrap(answers.issues, wrapOptions);

    var footer = filter([ breaking, issues ]).join('\n\n');

    commit(head + '\n\n' + body + '\n\n' + footer);
  });
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
