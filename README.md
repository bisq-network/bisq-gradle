# Bisq Gradle Tasks

Custom Gradle tasks for use across various Bisq repositories, to avoid build script duplication.

For example, the [Bisq Price Node](https://github.com/bisq-network/bisq-pricenode)
and [Bisq Monitor](https://github.com/bisq-network/bisq-monitor) repo build files place a startup
script and a lib directory in the root project directory.  Instead of duplicating the script
need to that, they apply from: [postBuild.gradle](task/postBuild.gradle).

## Usage

### Define git submodule 'bisq-gradle' in your repo

`$ git submodule add https://github.com/bisq-network/bisq-gradle.git`

This (1) pulls bisq-gradle, and (2) adds bisq-gradle to .gitmodules:
```asciidoc
    [submodule "bisq-gradle"]
        path = bisq
        url = https://github.com/bisq-network/bisq.git
```

### Link your repo to submodule

```asciidoc
$ git add bisq-gradle
$ git commit -m "Create submodule bisq-gradle"
$ git push
```


### Initialize submodule in your repo
```asciidoc
$ git submodule init
$ git submodule update
```

### Alternatively clone your repo with --recursive option
```asciidoc
$ git clone --recursive  your-repo.git   
```
