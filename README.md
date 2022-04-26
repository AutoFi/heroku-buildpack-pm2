# Heroku PM2 buildpack

This buildpack will install [PM2](https://github.com/unitech/pm2) on Heroku.

## Install

The node buildpack should be added first.

```
heroku buildpacks:set https://github.com/heroku/heroku-buildpack-nodejs
```

Add pm2 buildpack at index 2:

```
heroku buildpacks:add --index 2 https://github.com/AutoFi/heroku-buildpack-pm2

```

To start your node app with pm2, set the `"start"` command under `"scripts"` in package.json, or if you use a Procfile for heroku, the web 
command to the following:

```
pm2-runtime start ecosystem.config.js
```

You should have a `ecosystem.config.js` file to configure pm2. For example:

```
module.exports = {
	apps: [
		{
			name: 'myApp',
			script: './built/src/index.js',
			max_memory_restart: `${process.env.MAX_OLD_SPACE_SIZE}M` || '1024M',
			node_args: [
				'--optimize-for-size',
			],
		},
	],
};
```