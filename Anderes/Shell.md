`set -e` : Exit the script if an error happens

`set +e` : If get an error, it barfs out an error to the system (this is called an exit code) but the script will continue running

| Command | Description                                                  |
| ------- | ------------------------------------------------------------ |
| source  | to read and execute the content of a file (generally set of commands) |
|         |                                                              |
|         |                                                              |
|         |                                                              |
|         |                                                              |
|         |                                                              |
|         |                                                              |
|         |                                                              |
|         |                                                              |

### Install .deb file

```shell
sudo dpkg -i <file_name>.deb
# if any dependency error, run
sudo apt-get install -f
```

### Remove .deb file

```shell
sudo dpkg -r <file_name>.deb
```

