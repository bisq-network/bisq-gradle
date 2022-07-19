# Bisq Gradle Tasks

Custom Gradle tasks for avoiding some build script duplication across [bisq_network](https://github.com/bisq-network)
repositories.

The use of the first shared gradle task in this repo ([postBuild.gradle](task/postBuild.gradle)) is described below.

The [Bisq Price Node](https://github.com/bisq-network/bisq-pricenode)
and [Bisq Monitor](https://github.com/bisq-network/bisq-monitor) repo build files place a startup script and a lib
directory in the root project directory. Instead of duplicating script for that task, they link to this repo as a git
submodule, and execute [postBuild.gradle](task/postBuild.gradle).

## Usage

### Define git submodule 'bisq-gradle' in your repo

```asciidoc
$ git submodule add https://github.com/bisq-network/bisq-gradle.git
```

If you need to use a non-main branch of this repo, use the -b _branch-name_ option:

```asciidoc
git submodule add -b add-post-build-task https://github.com/ghubstan/bisq-gradle.git
```

This will add 'bisq-gradle' to .gitmodules:

```asciidoc
[submodule "bisq-gradle"]
    path = bisq-gradle
    url = https://github.com/bisq-network/bisq-gradle.git
```

### Link submodule 'bisq-gradle' in your repo

```asciidoc
$ git add bisq-gradle 
$ git commit -m "Add submodule bisq-gradle" bisq-gradle .gitmodules 
$ git push
```

### Register and clone new submodule 'bisq-gradle' in your repo

```asciidoc
$ git submodule init 
$ git submodule update
```

### Alternatively clone your repo with --recursive option

```asciidoc
$ git clone --recursive your-repo.git   
```

### Add task `postBuild` to your project's build:

```asciidoc
apply from: 'bisq-gradle/task/postBuild.gradle'
```

The `postBuild` task is configured to execute at the end of task `build`.
