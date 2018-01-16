# NPM semantic versioning

## Increment to the production minor version and push to git
```npm version minor -m "Upgrade to %s" ```


e.g. FROM v1.4.1-1 TO v1.5.0

## Go to the next pre minor release and push to git
```npm version preminor -m "Upgrade to %s"```


e.g. FROM v1.5.0 TO v1.6.0-0

## Increment the prerelease version and push to git
prerelease should be called after you run premajor, preminor, prepatch otherwiser it will assume its a patch

```npm version prerelease -m "Upgrade to %s"```


e.g. FROM v1.6.0-0 TO v1.6.0-1 TO v1.6.0-2 etc


```npm version [<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease | from-git]```


## pre and post verisoning steps

If preversion, version, or postversion are in the scripts property of the package.json, they will be executed as part of running npm version.

```
"scripts": {
  "preversion": "npm test",
  "version": "npm run build && git add -A dist",
  "postversion": "git push && git push --tags && rm -rf build/temp"
}
```
NOTE: version is run with the new version.