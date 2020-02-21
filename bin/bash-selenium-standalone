#/usr/bin/env/bash
set -e

###
# Install 'selenium standalone' server without any other dependencies installed.
#
# Why? Because I didn't want developer for maputnik to have to install anything except docker/docker-compose.
#
# Caveat: Yes you do need 'java' and 'curl' but almost all users will have that installed already.
###
uname_out="$(uname -s)"
case "${uname_out}" in
    Linux*)  machine=linux;;
    Darwin*) machine=mac;;
    *)       machine="UNKNOWN"
esac

if [[ "$machine" == "UNKNOWN" ]]; then
  >&2 echo "Error: Unknown machine '${uname_out}'"
  exit 1
fi

cleanup=0

while getopts ":hv-:" opt; do
  case $opt in
    -)
      case "${OPTARG}" in
        cleanup)
          cleanup=1
          shift 1
        ;;
      esac;;
  esac
done

cache_dir=".bash-selenium-cache"


selenium_standalone_version="3.141.5"
geckodriver_version="0.23.0"
chromedriver_version="2.43"

mkdir -p "$cache_dir";
geckodriver_path="$cache_dir/geckodriver"
chromedriver_path="$cache_dir/chromedriver"
selenium_standalone_path="$cache_dir/selenium-standalone.jar"

if [ "$cleanup" -gt 0 ]; then
  >&2 echo "Cleaning up..."
  if [ -f "$geckodriver_path" ]; then
    >&2 echo "Removing: ${geckodriver_path}"
    rm "$geckodriver_path";
  fi

  if [ -f "$chromedriver_path" ]; then
    >&2 echo "Removing: ${chromedriver_path}"
    rm "$chromedriver_path";
  fi

  if [ -f "$selenium_standalone_path" ]; then
    >&2 echo "Removing: ${selenium_standalone_path}"
    rm "$selenium_standalone_path";
  fi
fi

if [ -z "$(which java)" ]; then
  >&2 echo "ERROR: You need to have 'java' installed"
  exit 1
fi

if [ -f "$geckodriver_path" ]; then
  >&2 echo "Found: $geckodriver_path"
else
  >&2 echo "Downloading geckodriver to: $geckodriver_path"

  case "${machine}" in
    linux*) arch=linux;;
    mac*)   arch=macos;;
  esac

  cd "$cache_dir"
    rm -f temp.tar.gz
    curl -# -o temp.tar.gz -L "https://github.com/mozilla/geckodriver/releases/download/v${geckodriver_version}/geckodriver-v${geckodriver_version}-${arch}.tar.gz"
    tar xzvf temp.tar.gz
    rm temp.tar.gz
  cd -
fi

if [ -f "$chromedriver_path" ]; then
  >&2 echo "Found: $chromedriver_path"
else
  >&2 echo "downloading chromedriver to: $chromedriver_path"

  case "${machine}" in
    linux*) arch=linux64;;
    mac*)   arch=mac64;;
  esac

  cd "$cache_dir"
    rm -f temp.zip
    curl -# -o temp.zip -L "https://chromedriver.storage.googleapis.com/${chromedriver_version}/chromedriver_${arch}.zip"
    unzip temp.zip
    rm temp.zip
  cd -
fi

if [ -f "$selenium_standalone_path" ]; then
  >&2 echo "Found: $selenium_standalone_path"
else
  >&2 echo "downloading selenium standalone server to: $selenium_standalone_path"

  cd "$cache_dir"
    curl -# -L https://selenium-release.storage.googleapis.com/3.141/selenium-server-standalone-${selenium_standalone_version}.jar -O
    mv "selenium-server-standalone-${selenium_standalone_version}.jar" selenium-standalone.jar
  cd -
fi

java \
  -Dwebdriver.chrome.driver="./$chromedriver_path" \
  -Dwebdriver.gecko.driver="./$geckodriver_path" \
  -jar "$selenium_standalone_path" \
  "$@"

