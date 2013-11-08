dev
===========

* [What is perspective?](http://perspective.github.io/perspective/)
* [What is the goals of perspective?](http://perspective.github.io/perspective/goals.html)
* [How to contribute](#how-to-contribute)
	* Contribution guidelines pr. role
	* Setting up your dev environment
* [Design principles](#design-principles)
* [Architecture](#architecture)

How to contribute
-----------------------------
Note: due to dependency on rethinkdb, there's currently no support for running on platforms other than linux/mac.

### Everyone
1. Start with an [issue](https://github.com/perspective/perspective-client/issues). Does the feature/bug you seek exist?
    * No? [Create a new issue](https://github.com/perspective/perspective-client/issues/new) and start a discussion on what you want to implement
  	* Yes? Is someone working on it already? Contribute in the discussion and see if you can help out

### Designer/UX Designer?
1. Look at existing enhancements and issues and contribute with sketches, designs, ideas
2. Create issues on existing functionality and upload sketches, designs, ideas

### Business analyst/Team leader?
1. Analyse what kind of information different stakeholders need on a ongoing project
2. Do they need the same information at all times? What's relevant at a given time in the project?
3. What can we do to make perspective a suitable application for information sharing in a development project?
4. Perspective strategy

### Developer?

#### On new apps/modules/integration points
1. Suggest a new project in the issue list on GitHub
2. Get the perspective members to create a repository
3. Follow the guidelines below for "existing code"

#### Existing code
1. Fork the desired repositores you want to improve
2. Do your magic
3. Open a pull request when:
	* The work is stable
	* Test coverage is in place

#### Setting up your dev environment

1. Install node.js
2. Install bower with `npm install -g bower`
3. Install nodemon with `npm install -g nodemon` to make servers reload on change
4. Install rethinkdb
   Note: rethinkdb can only run on linux/mac hosts. On windows, run a virtual server and make sure to expose ports 8080, 28015 and 29015 from this.
5. Clone all modules, as described below.

To ease the process of handling multiple repositories, we recommend using [myrepos](https://github.com/joeyh/myrepos). Simply put [mr](https://github.com/joeyh/myrepos/blob/master/mr) on your `PATH` and you are good to go:

1. `mkdir perspective`
2. `curl -o .mrconfig https://raw.github.com/perspective/dev/master/.mrconfig.example`
3. `touch ~/.mrconfig`
4. (review the .mrconfig file)
5. ``echo `pwd`/.mrconfig >> ~/.mrtrust``
    To avoid a warning later.
6. `mr checkout`  
    will git clone all modules
7. `mr link`  
    will invoke `npm link` in correct order on each module. 
8. `mr install`
    will invoke `npm install` in correct order on each module.

By now you should have:

	perspective
	|── dev - development tools and documentation
	|── perspective - the website
	|── perspective-client - front-end web client connecting to different backend apps (jenkins, tasks)
	├── perspective-core - shared core components between web client and backend apps
	├── perspective-core-db - component for connecting to the perspective db, uses rethinkdb
	├── perspective-core-rest - component for a simplified process of creating REST APIs
	├── perspective-core-server - shared core components for every backend apps
	├── perspective-core-web-socket - component for a simplified process of creating web-socket support
	├── perspective-core-web-socket-helper - shared component between the perspective client and perspective-core-web-socket
	├── perspective-jenkins - a jenkins backend app
	├── perspective-tasks - a task manager backend app
	└── startup-scripts - startup scripts for perspective on different os

Other useful `mr` commands are:

* `mr update` to run `git pull` on all modules
* `mr status` to run `git status` on all modules
* ... you get the point. See `mr help` for more info.

Verify that the settings in perspective-jenkins/dev.sh, perspective-tasks/dev.sh and perspective-client/dev.sh match your environment.

#### Boot the back and make them reload on changes:
1. Run `rethinkdb`
2. `cd perspective-jenkins && ./dev.sh`
3. `cd perspective-tasks && ./dev.sh`

#### Boot frontend
1. `cd perspective-client`
2. `npm install`
3. `bower install`
4. `make.js`
5. `./dev.sh`

Design principles
-----------------

* We strive to follow the principles of [12 factor apps](http://12factor.net/)
	* Inter-application-communication are [treated as attached resources](http://12factor.net/backing-services)
	* Config is stored as environment variables. (see `dev.sh` in perspective-jenkins and perspective-tasks)
* We're inspired by [Spotify](https://dl.dropboxusercontent.com/u/1018963/Articles/SpotifyScaling.pdf):
	* Application/component silos in backend, with expert teams pr. feature --> apps (perspective-jenkins, perspective-tasks)
	* One front-end app pr. platform --> (perspective-client)
* As we're developing a tool for software development teams, we can afford to live on the cutting edge of technology. One of perspective's goals is to be hackable and a fun place to test new technology. Currently we are using:
	* Front-end:
		* Ractive.js for two-way binding, along with Object.observe (only supported in Chrome with experimental JavaScript features enabled)
		* Page.js for simplistic routing
		* Superagent for making http requests
		* Websockets
	* Back-end:
		* Node.js as backend language
		* RethinkDB for data storage
		* Docker for deployment

Architecture
-----------------

![perspective architecture](https://raw.github.com/perspective/dev/master/perspective_architecture.png "")

The ***web client*** is a standalone application that provides perspectives only front-end at the moment.
It communicates with back-end applications such as ***perspective-tasks*** and ***perspective-jenkins*** over HTTP/REST and WebSockets.
Back-end applications may rely on several components, such as ***perspective-core-db*** and ***perspective-core-rest***.

As both the front-end and back-end is written in JavaScript, we are able to share some code as seen in ***perspective-core***


License
-------

MIT
