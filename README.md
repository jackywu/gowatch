# gowatch

Golang program real-time compilation tools to enhance development efficiency

Real-time compilation by monitoring file changes in a specified directory

### install

```go
go get github.com/jackywu/gowatch
```

After the installation is complete, you can use the `gowatch` command to execute in the main package:

**screenshot：**
![gowatch](./screenshot/gowatch.png)


### Command line parameters

- -o : Optional，specify the target build path
- -p : Optional，Specified the need to build the package, which can also be a single file
- -g : Optional, specify the time gap during which gowatch will ignore any file modification event
- -x : Optional, specify the file's modification event will be ignored which match the regex-pattern

**example:**

simple example:
`gowatch -o cmd/apiserver.go -p cmd/apiserver`

with args:
`gowatch -o cmd/apiserver.go -p cmd/apiserver -args "start --binding-address=0.0.0.0"`

exclude *_test.go file:
`gowatch -o cmd/apiserver.go -p cmd/apiserver -x ".*_test.go" -args "start --binding-address=0.0.0.0 --binding-port=1234"`

with time gap(in 60 seconds, any file modification event will be ignored):
`gowatch -o cmd/apiserver.go -g 60 -p cmd/apiserver -x ".*_test.go" -args "start --binding-address=0.0.0.0"`

### config file

`gowatch.yml`

Most of the time, you do not need to change the configuration to do most of what you need to do with the `gowatch` command, but it also provides some configuration for customizing. Create the` gowatch.yml` file in the executable:

```
# gowatch.yml Configuration example

# The name of the generated executable file, the default is the current directory name
appname: "test"
# specify the compiled target file directory
output: /bin/demo
# Need to monitor the additional file name suffix, the default only '.go' file
watch_exts:
    - .yml
# need to monitor the directory, the default only the current directory
watch_paths:
    - ../pk
# when the program is executed, additional parameters need to be added
cmd_args:
    - arg1=val1
# need to increase the additional environment variables, the default has been loaded by the current environment variables
envs:
    - a=b
# whether to monitor the 'vendor' folder under the file changes
vendor_watch: false
# do not need to listen to the directory
excluded_paths:
    - path
# do not watch these file which match the regex-pattern
ExcludedPattern: ""
# main package path, can also be a single file, multiple files separated by commas
build_pkg: ""
# build tags
build_tags: ""

# any file modification event will be ignored during this time gap, unit: second
BuildGap: 0
```




>Inspired by [bee](https://github.com/beego/bee)
