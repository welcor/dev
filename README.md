dev
===========

## Contributing

### Assembling modules
While developing you'll need to:

1. Clone the desired modules
2. Run `npm link` inside each module in the correct order to setup symlinks

To ease this process, we recommend using [myrepos](https://github.com/joeyh/myrepos) - a tool to handle multiple repositories at once. Simply put [mr](https://github.com/joeyh/myrepos/blob/master/mr) on your `PATH` and you are good to go:

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
	|── perspective-api
	├── perspective-api-jenkins
	├── perspective-api-tasks
	├── perspective-api-views
	├── perspective-client
	├── perspective-core
	├── perspective-dev
	└── perspective-startup-scripts

Other useful `mr` commands are:

* `mr update` to run `git pull` on all modules
* `mr status` to run `git status` on all modules
* ... you get the point. See `mr help` for more info.

### Boot the server and make it reload on changes:
1. `cd perspective-api`
2. `rethinkdb`
3. Open new tab, also in `perspective-api`
4. `npm install -g nodemon`
5. `nodemon bin/perspective-api.js`

### Boot frontend
1. `cd perspective-client`
2. `npm install`
3. `./server.js`

License
-------

MIT