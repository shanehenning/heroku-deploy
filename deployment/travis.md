
#### Install travis
Create an account on https://travis-ci.org/ and login  


(need ruby 2.0)  
ruby -v
**Installing ruby**
windows: http://rubyinstaller.org/
mac: check ruby -v should be v2

more information https://github.com/travis-ci/travis.rb#installation  
`gem install travis -v 1.8.2 --no-rdoc --no-ri`   

If you have permission errors with the above command use sudo:   
`sudo gem install travis`  

`travis version`  
"Shell completion not installed. Would you like to install it now? |y| y"  

should be 1.8.2

#### add npm scripts to package.json
```
"scripts": {
  "test": "./node_modules/mocha/bin/mocha",
  "start": "node index.js",
  "lint": "./node_modules/eslint/bin/eslint.js *"
}
```

#### create a travis config 'travis.yml'
use the .travis.yml (should noT be git ignored) -  you can modify but be careful to keep format
The "addons" sections is needed for mongo and bcrypt. Remove bcrypt source and package if you don't need it as it slows down build.

```
language: node_js
node_js:
  - 4
services:
  - mongodb
addons:
  apt:
    sources:
    - mongodb-3.2.4-precise
    packages:
    - mongodb-org-server
    sources:
    - ubuntu-toolchain-r-test
    packages:
    - gcc-4.8
    - g++-4.8
env:
  - CXX=g++-4.8
sudo: required
install:
  - npm install -g eslint mocha chai
before_script: npm install
script:
  - npm run test
  - npm run lint
```

`travis lint`   checks that your travis file is OK  
"Hooray, .travis.yml looks valid :)"  

known issue with travis lint when you have addons:  
https://github.com/travis-ci/travis-ci/issues/3694

## From within the git project folder:

#### Login
`travis login`  use github login  

#### Enable travis for this repo
`travis enable`  
"detected repository is xxxx, is this correct yes|no
triggering sync"  


`travis open`   
Opens to browser - if you're logged in to the browser you'll get to this repo

You can add status image to your README.md - will tell if you're passing tests on most recent push
click on "unknown" next to "build" and choose markdown 9:22
copy to your README.md

`git push`  pushing to git should activate a build on travis  
`travis open`  go watch the build  - click on branches to see the build in process  

Duncan made a video on using travis: https://www.youtube.com/watch?v=n9fgZad0TIo&feature=youtu.be
