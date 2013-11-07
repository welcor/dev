dev
===========

* What is perspective?
* What is the goals of perspective?
* How to contribute
	* Contribution guidelines
	* Setting up your dev environment
* Design principles
* Architecture

How to contribute
-----------------------------

### Guidelines
1. Start with an [issue](https://github.com/perspective/perspective-client/issues). Does the feature/bug you seek exist?
	* No? [Create a new issue](https://github.com/perspective/perspective-client/issues/new) and start a discussion on what you want to implement
	* Yes? Is someone working on it already? Contribute in the discussion and see if you can help out
2. Fork the desired repositores you want to improve
3. Do your magic
4. Open a pull request when:
	* The work is stable
	* Test coverage is in place

### Setting up your dev environment

1. Install node.js
2. Install bower with `npm install -g bower`
3. Install nodemon with `npm install -g nodemon` to make servers reload on change
4. Install rethinkdb
5. Clone all modules, as described below.

To ease the process of handling multiple repositories, we recommend using [myrepos](https://github.com/joeyh/myrepos). Simply put [mr](https://github.com/joeyh/myrepos/blob/master/mr) on your `PATH` and you are good to go:

1. `mkdir perspective`
2. `curl -o .mrconfig https://raw.github.com/perspective/dev/master/.mrconfig.example`
3. (review the .mrconfig file)
4. `mr checkout`  
    will git clone all modules
5. `mr link`  
    will invoke `npm link` in correct order on each module. Note: you probably get a warning here requiring you to add the path to `...perspective/.mrconfig` file to `~/.mrtrust`.
6. `mr install`
    will invoke `npm install` in correct order on each module.

By now you should have:

	perspective
	|── dev
	|── perspective
	|── perspective-client
	├── perspective-core
	├── perspective-core-db
	├── perspective-core-rest
	├── perspective-core-server
	├── perspective-core-web-socket
	├── perspective-core-web-socket-helper
	├── perspective-jenkins
	├── perspective-tasks
	└── startup-scripts

Other useful `mr` commands are:

* `mr update` to run `git pull` on all modules
* `mr status` to run `git status` on all modules
* ... you get the point. See `mr help` for more info.

### Boot the back and make them reload on changes:
1. Run `rethinkdb`
2. `cd perspective-jenkins && ./dev.sh`
3. `cd perspective-tasks && ./dev.sh`

### Boot frontend
1. `cd perspective-client`
2. `npm install`
3. `bower install`
4. `./dev.sh`


Design principles
-----------------

* We strive to follow the principles of [12 factor apps](http://12factor.net/)
* As we're developing a tool for software development teams, we afford to live on the cutting edge of technology. One of perspective's goals is to be hackable and a fun place to test new technology. Currently we are using:
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
* TODO


License
-------

MIT