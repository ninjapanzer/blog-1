Hello everyone!!

Often we get queries/requests on how someone can help with the documentation, and how they can set up the docs application on their local machine so as to see changes immediately on their screen before issuing a pull request with their changes.

This blog post outlines how to set up our docs app and how you can help with the documentation effort. 

### Overview
Our documentation is split into two repositories:
- [Docs App](https://github.com/phalcon/docs-app). This repo contains the application that handles our documentation (templates, CSS, etc.).
- [Docs](https://github.com/phalcon/docs). This repo contains the actual articles that are shown on screen (content).

These repositories have been set up to work together to offer an easy way to set up and maintain the documentation.

The `docs` repository has also been integrated with [Crowdin](https://crowdin.com), which handles all the translation efforts of our documentation.

### Setup
So you want to set up the docs application to have the documents application running on your local machine. Great! The steps are:

- Fork the `docs-app` repository 
- Fork the `docs` repository 
- Clone the `docs-app` to your machine.
- Install [nanobox](https://nanobox.io) if you don't have it
- Setup the `.env` file
- Change the `deploy` script
- Setup the app using nanobox
- Run the `deploy` script
- Run the app with nanobox
- Launch the app on your browser :) 

#### Fork the repositories
If you haven't done so already, fork the repositories from the phalcon github organization page [https://github.com/phalcon](https://github.com/phalcon). You will need the `docs-app` and `docs` repositories.

#### Clone the `docs-app` repository
In a suitable location on your machine clone the `docs-app` repository (the fork)

```bash
$ git clone git@github.com:niden/docs-app
```

##### **NOTE** Your repository URL will be different than the above command {.alert .alert-warning}

#### Install `nanobox`
If you haven't done so already, visit [nanobox.io](https://nanobox.io) and download and install the application. It will ask you some basic questions (usually we use docker as the engine instead of Virtualbox) as part of its setup.

#### Setup the `.env` file
In the `docs-app` folder (or wherever you have cloned the `docs-app` repository), make a copy of the `.env.example` file and rename it to `.env`. Open the file and edit the `APP_URL` entry with a local domain. In this example we use `docs.phalcon.ld`.

#### Change the `deploy` script
Open the `deploy` script and change the `DOCS_REPO` entry to your fork of the `docs` repo. For example it will be something like this:

```bash
git@github.com:niden/docs
```

#### Setup the app using nanobox
In your folder (where you cloned `docs-app`) run the following command in a terminal:

```bash
$ nanobox run
```

After a while you will see something like this:

```bash
$ nanobox run
Preparing environment :

docs-app (local) :
...

Preparing environment :
...

Building dev environment :
  ✓ Starting docker container
  ✓ Configuring


      **
   *********
***************   Your command will run in an isolated Linux container
:: ********* ::   Code changes in either the container or desktop are mirrored
" ::: *** ::: "   ------------------------------------------------------------
  ""  :::  ""     If you run a server, access it at >> 172.18.0.4
    "" " ""
       "
```

Once nanobox finishes its tasks, you will be "inside" the container. Your prompt will be:

```bash
/app $
``` 

Type `exit` to exit the container.

Run the following command to create a `hosts` entry for your environment so that you can use the local domain:

```bash
$ nanobox dns add local docs.phalcon.ld
```

This command will be different in your system, depending on the name you chose for your local domain.

#### Run the `deploy` script
In the same terminal, (root folder of `docs-app`) run the `deploy` script

```bash
$ ./deploy
```

This script will start cloning the `docs` repository branches needed under the `./docs` folder of your `docs-app` application (mind boggling - too many `docs`! :D). The output on the terminal will provide information about the process.

#### Run the app with nanobox
Run the following command:

```bash
$ nanobox run php-server
```

#### Launch the app in your browser
Open the `http://docs.phalcon.ld` URL in your browser and voila!!!

### Modifications
If you wish to make changes to the application (`docs-app`), stylesheets or layout, feel free to do so and issue a pull request in the `docs-app` Phalcon repository.

You can also help with some of the English text located in the `en` folder under each version folder (`docs/3.2/en`, `docs/3.1/en`, etc.). These changes will be sent to the `docs` Phalcon repository.

##### Changes to a docs file (markdown) in any language other than English will not be accepted {.alert .alert-danger}

### Translations
For languages other than English, you will need to use Crowdin Project for the documentation:

[https://crowdin.com/project/phalcon-documentation](https://crowdin.com/project/phalcon-documentation)

The translated strings will be brought into the documentation via pull requests from Crowdin.

Enjoy!!


<3 Phalcon Team

