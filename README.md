# bash-selenium-standalone
A single bash script to download/install/run selenium standalone

[![stability-experimental](https://img.shields.io/badge/stability-experimental-orange.svg)][stability]

[stability]:   https://github.com/orangemug/stability-badges#experimental


## Usage
The following will download

 - selenium-standalone
 - chromedriver
 - geckodriver

Then `selenium-standalone` will be started passing any args along to `selenium-standalone`

```
./bash-selenium-standalone
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
