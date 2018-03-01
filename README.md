# cube-application-guide

> A guide for cube application

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

## Guide

### Stage-1

Use vue-cli to init a cube-template by the following command.

```shell
# Generate a cube project in current directory 
vue init cube-ui/template

# Or generate a cube project in the special sub directory
vue init cube-ui/template some-sub-directory
```

Then, you will see several ask to let you choose what kind of features you want.

As in this application, we need only two or three component of cube-ui, so we chose `importTyoe` as `partly`, the details is following.

```
$ vue init cube-ui/cube-template

Generate project in current directory? Yes
  A newer version of vue-cli is available.

  latest:    2.9.3
  installed: 2.8.2

? Project name cube-application-guide
? Project description A guide for cube application
? Author AmyFoxFN <funan_amy@foxmail.com>
? Vue build runtime
? Use post-compile? Yes
? Import type Partly
? Custom theme? Yes
? Use rem layout? No
? Install vue-router? No
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Set up unit tests No
? Setup e2e tests with Nightwatch? No

   vue-cli · Generated "cube-application-guide".

   To get started:

     npm install
     npm run dev

   Yeah,let's make an awesome app via cube-ui!

```

Now, you can run the `npm install` and `npm run dev` to see if it works!

Yeah, let's make an awesome app via cube-ui!

### Stage 2

For our application, the main parts is a slide to switch between tabs and the scroll in each tab.

And we will code the two main parts in Stage 2 and Stage 3.

### Stage 3


