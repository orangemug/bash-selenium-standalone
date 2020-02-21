# bash-selenium-standalone
A single bash script to download/install/run selenium standalone

[![stability-experimental](https://img.shields.io/badge/stability-experimental-orange.svg)][stability]

[stability]:   https://github.com/orangemug/stability-badges#experimental


## Prerequisites
The requirements should be available on most systems, you'll get a friendly error if they are not available.

 - `bash`
 - `curl`
 - `java` - required by selenium-standalone



## Install
Add `./bin/bash-selenium-standalone` to your `PATH` (see <https://unix.stackexchange.com/a/26059>) or just run it with

```
./bin/bash-selenium-standalone
```


## Usage
The following will download

 - selenium-standalone
 - chromedriver
 - geckodriver

Then `selenium-standalone` will be started passing any args along to `selenium-standalone.jar`

```
./bash-selenium-standalone [options]
```

The files will be saved to a `.bash-selenium-standalone` directory where you ran the script from.

```
$ find .bash-selenium-cache
.bash-selenium-cache
.bash-selenium-cache/selenium-standalone.jar
.bash-selenium-cache/geckodriver
.bash-selenium-cache/chromedriver
```

## License
MIT
