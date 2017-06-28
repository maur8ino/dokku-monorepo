bootlegged dokku-monorepo
===============

Dokku plugin for monorepo setups.

## Install

```
dokku plugin:install https://github.com/PAStheLoD/dokku-monorepo
```

## Usage

```
$ ls
.dokku-monorepo
myapp1
myapp2
```

The file .dokku-monorepo contains paths for applications to be deployed:
```
# watch out for ordering, put the less specific (shorter) name at the end

app-worker=myapp2/backend
app=myapp1
```

The part before `=` is used to identify the dokku application. For example, here:
```
$ git remote -v
app             dokku@dokku.me:example-app
app-worker      dokku@dokku.me:example-app-worker
```

the `example-first` and `example-staging-first` applications would be deployed from the `myapp1` folder.

When you push the code to an application's remote, the folder gets detected for you:
```
$ git push first
Counting objects: 253, done.
Writing objects: 100% (253/253), 38.27 KiB | 0 bytes/s, done.
Total 253 (delta 117), reused 233 (delta 109)
=====> Monorepo detected
=====> Installing from ./myapp1
-----> Cleaning up...
-----> Building example-first from herokuish...
-----> Adding BUILD_ENV to build environment...
-----> Python app detected
       ...
```

It's that easy!

### Dockerfile in subfolder

By default Dokku only looks for Dockerfiles in the root of the repository. If one/all of your applications are deployed with a Dockerfile, you can use the [dokku-dockerfile](https://github.com/mimischi/dokku-dockerfile) plugin to point Dokku to the right folder.
