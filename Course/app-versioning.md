### Application versioning:
* `1 . 4 . 2` - Semantic numbering (Major . Minor . Patch)
* `Major changes` - related to incompatible API changes
  * Replaced Framework
  * New feature
* `Minor changes` - new functionality in a backward-compatible manner
  * New, minor feature
  * Bigger Bugfix
* `Patch changes` - related to small bugfixes & changes, which are backward compatible
  * Small changes
  * Bugfix

### Dynamic Versioning:
* Dynamically set an incremented version when we build the Docker image

### Pass Env Vars as Dotenv Artifact:
* Best practise when use 5 or more env variables
* `Dotenv file` is a lightweight npm package that automatically loads 
environment variables from a .env file into the process
* Change in build_image:
  * instead of `- echo $VERSION > version-file.txt`
  * type `- echo "VERSION=$VERSION" >> build.env`
* `Dotenv artifact` - Save the .env file as a dotenv artifact
  * `artifacts: reports: dotenv: build.env`
* Usage of these env vars:
  * Collected variables are registered as runtime-created variables of the job
  * Jobs in later stages can use the variable in scripts
    * No need to `- export VERSION=$(cat version-file.txt)` in push_image or deploy_to_dev - auto export
    * No need to download artifacts cause they are env variables already - auto export