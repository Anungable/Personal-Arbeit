### Switch between different SW versions

**JAVA**

```bash
#列出有的版本
update-java-alternatives --list

#切換版本
sudo update-java-alternatives --set /usr/lib/jvm/java-1.8.0-openjdk-amd64
```

**GCC**

```bash
#配置版本＋設定最高優先權
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 90 --slave /usr/bin/g++ g++ /usr/bin/g++-9 --slave /usr/bin/gcov gcov /usr/bin/gcov-9

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 70 --slave /usr/bin/g++ g++ /usr/bin/g++-7 --slave /usr/bin/gcov gcov /usr/bin/gcov-7

#修改最高優先權
sudo update-alternatives --config gcc
```

### Remove a package

**a specific version of java**

```shell
dpkg --list | grep jdk
sudo apt remove jdk-13*
```

