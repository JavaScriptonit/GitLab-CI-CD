## Optimize CI/CD Pipeline & Configure Multi-Stage Pipeline

### Configure Caching to speedup Pipeline execution:
* Artifacts:
  * Job artifacts get uploaded and saved on the **GitLab server**
  * Use artifacts to pass intermediate build results between stages
* Cache:
  * Use cache for dependencies, like packages you download from the internet
  * Cache is stored on the **GitLab Runner**
* Distributed Cache:
  * Central cache storage
  * Download from remote storage again over the internet
  * Still faster to download 1 zip file, instead of each dependency separately


* Cache key:
  * Give each cache a unique idenfying key
  * If not set, the default key is "default"
  * All jobs that use the same cache key use the same cache
* Cache path:
  * Used to choose which files or directories to cache
  * You can use an array of paths relative to the project directory
* Cache policy:
  * Pull-push:
    * Job downloads the cache when the job starts & uploads changes to the cache when the job ends
    * The default policy
  * Pull:
    * To only download the cache, but never upload the changes
    * Use when you have many jobs executing in parallel that use the same cache

### Best Practise:
* Not **depend** on cache to be available
* Caching is an optimization, but it isn't guaranteed to always work

### Configure Volume for Docker Executor:
* in .gitlab-ci.yaml cache gets created inside the container on the Docker Runner
* Job get executed inside a new Docker container
* When the job finishes, the container is removed
* Configure Volume:
  * `$ sudo ls /etc/gitlab-runner/` - config.toml - the configuration file with 2 Runners
  * `$ sudo vim /etc/gitlab-runner/config.toml` - to configure it with [VIM editor](https://sites.google.com/site/voipnotes/l/vim-editor-commands-1)
    * [Useful Vim Commands on YouTube.com](https://www.youtube.com/watch?v=yfxRHSSGgSg)
  * `cache_dir = "/cache"` - add same location to cache as volume directory
  * `:wq` - Save the file

### Clear the Cache:
* Manually with button "Clear runner caches"
  * The old cache is not deleted
  * Cache name will be updated and used instead
  * Have to delete manually files from the Runner storage
  * Format "cache-index", index is incremented by one
* Change the value for the cache key in yml file

* `$ docker volume ls` - reference to the physical location on this machine where cache is stored
* `$ runner-ieinwck3-project-40450508-concurrent-0-cache-3c3f060a0374fc8bc39395164f415a70` - the location "/var/lib/docker/volumes/runner-ieinwck3-project-40450508-concurrent-0-cache-3c3f060a0374fc8bc39395164f415a70/_data"
* `sudo ls /var/lib/docker/volumes/runner-ieinwck3-project-40450508-concurrent-0-cache-3c3f060a0374fc8bc39395164f415a70/_data/JavaScriptonit/mynodeapp-cicd-project` - path of the cache
* [Where the caches are stored](https://docs.gitlab.com/ee/ci/caching/) - for Shell, Docker and Docker Machine
* 