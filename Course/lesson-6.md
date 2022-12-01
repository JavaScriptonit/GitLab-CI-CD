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