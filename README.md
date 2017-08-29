# Gitbot
![GUNDAM image](help/gundam.jpg)
![GUNDAM image](help/gundam.jpg)

[![Build Status Master branch](https://travis-ci.org/openSUSE/gitbot.svg?branch=master)](https://travis-ci.org/openSUSE/gitbot)

## Gitbot: automatize your Prs testing with your custom test env.
Gitbot allow you to run tests on prs. It run on each Systems that support ruby and octokit.

### Read real examples

[Real example](help/real_examples.md)

# Why gitbot?

Gitbot was developed. to run jenkins job against a repo.
It differs from travis because it's not limited on container or others limited env, it just run everywhere.

Like in custom jenkins server or vms(OS indipendent), or in custum containers.


## 1) Installation:

```console
gem install octokit
gem install netrc
```

## 2) Configuration:

The **only one** config is to have a valid ``` /~.netrc``` file and the user has to have **read access credentials** to the repo you want to test.
Configure the netrc file like this:

```
machine api.github.com login MY_GITHUB_USE password MY_PASSWORD
```

### 3) run it : 
```console
echo "#! /bin/bash" > /tmp/tests.sh
chmod +x tests.sh
ruby gitbot.rb -r openSUSE/gitbot -c "ruby-test" -d "ruby-gitbot-tuto" -g /tmp/pr-ruby01/ -t /tmp/tests.sh -f ".rb"
```


### Documentation


#### Basic design
Basically gitbot run a validation script/commands (-t) (could be bash, python, ruby, etc) against each open PR of your XXX Branch.

All open Pull-request will be then scanned for modifications on specific file type modified (-f ".py" as example). 
If the pr doesn't modify a python file( -f '.py') gitbot doesn't run a test against the pr.

If you have 10 untested PRs, you have to run it 10 times. 
Gitbot was especially so designed, because 1 run equals a 1 Jenkins Job.

The context  -c  is important: **make an unique context name** for each test category you want to run.
If you have same context name and the pr was already reviewed by gitbot, test will be not triggered.

EXAMPLE: 
```-c "python-pyflake", -c 'python-unit-tests'```

The context trigger the exec. of tests.

For more doc refer to [Documentation](doc/README.md)

#### Advanced documentation

- Retrigger the jobs. [Advanced_doc](doc/ADVANCED.md)

************************************************
