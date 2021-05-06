# OneDrive Client for Linux
[![Version](https://img.shields.io/github/v/release/abraunegg/onedrive)](https://github.com/abraunegg/onedrive/releases)
[![Release Date](https://img.shields.io/github/release-date/abraunegg/onedrive)](https://github.com/abraunegg/onedrive/releases)
[![Travis CI](https://img.shields.io/travis/com/abraunegg/onedrive)](https://travis-ci.com/abraunegg/onedrive/builds)
[![Docker Build](https://img.shields.io/docker/cloud/automated/driveone/onedrive)](https://hub.docker.com/r/driveone/onedrive)
[![Docker Pulls](https://img.shields.io/docker/pulls/driveone/onedrive)](https://hub.docker.com/r/driveone/onedrive)

A free Microsoft OneDrive Client which supports OneDrive Personal, OneDrive for Business, OneDrive for Office365 and SharePoint.

This powerful and highly configurable client can run on all major Linux distributions, FreeBSD, or as a Docker container. It supports one-way and two-way sync capabilities and securely connects to Microsoft OneDrive services.

This client is a 'fork' of the [skilion](https://github.com/skilion/onedrive) client which was abandoned in 2018.

## Features
*   State caching
*   Real-Time file monitoring with Inotify
*   File upload / download validation to ensure data integrity
*   Resumable uploads
*   Support OneDrive for Business (part of Office 365)
*   Shared Folder support for OneDrive Personal and OneDrive Business accounts
*   SharePoint / Office365 Shared Libraries
*   Desktop notifications via libnotify
*   Dry-run capability to test configuration changes
*   Prevent major OneDrive accidental data deletion after configuration change
*   Support for National cloud deployments (Microsoft Cloud for US Government, Microsoft Cloud Germany, Azure and Office 365 operated by 21Vianet in China)

## What's missing
*   While local changes are uploaded right away, remote changes are delayed until next automated sync cycle when using --monitor
*   Ability to encrypt/decrypt files on-the-fly when uploading/downloading files from OneDrive
*   Support for Windows 'On-Demand' functionality so file is only downloaded when accessed locally
*   A GUI for configuration management

## Frequently Asked Questions
Refer to [Frequently Asked Questions](https://github.com/abraunegg/onedrive/wiki/Frequently-Asked-Questions)

## Reporting issues
If you encounter any bugs you can report them here on Github. Before filing an issue be sure to:

1.  Check the version of the application you are using `onedrive --version` and ensure that you are running either the latest [release](https://github.com/abraunegg/onedrive/releases) or built from master.
2.  Fill in a new bug report using the [issue template](https://github.com/abraunegg/onedrive/issues/new?template=bug_report.md)
3.  Generate a debug log for support using the following [process](https://github.com/abraunegg/onedrive/wiki/Generate-debug-log-for-support)
4.  Upload the debug log to [pastebin](https://pastebin.com/) or archive and email to support@mynas.com.au

## Known issues
Refer to [docs/known-issues.md](https://github.com/abraunegg/onedrive/blob/master/docs/known-issues.md)

## Documentation and Configuration Assistance
### Building and Installation
Refer to [docs/INSTALL.md](https://github.com/abraunegg/onedrive/blob/master/docs/INSTALL.md)

### Configuration and Usage
Refer to [docs/USAGE.md](https://github.com/abraunegg/onedrive/blob/master/docs/USAGE.md)

### Configure OneDrive Business Shared Folders
Refer to [docs/BusinessSharedFolders.md](https://github.com/abraunegg/onedrive/blob/master/docs/BusinessSharedFolders.md)

### Configure SharePoint / Office 365 Shared Libraries (Business or Education)
Refer to [docs/SharePoint-Shared-Libraries.md](https://github.com/abraunegg/onedrive/blob/master/docs/SharePoint-Shared-Libraries.md)

### Configure National Cloud support
Refer to [docs/national-cloud-deployments.md](https://github.com/abraunegg/onedrive/blob/master/docs/national-cloud-deployments.md)

### Docker support
Refer to [docs/Docker.md](https://github.com/abraunegg/onedrive/blob/master/docs/Docker.md)

### 启动http、https、ftp代理
设置命令行下所有的其它程序使用socks代理，安装一个privoxy代理工具，实现终端内socks5转换为http/https，进而将http/https请求转发
给ss，实现终端内的代理
- sudo apt-get install privoxy

配置/etc/privoxy/config文件
- 保证存在下面两行存在, forward-socks5t 如果不行就改成 forward-socks5 
- listen-address localhost:8118
- forward-socks5t / 127.0.0.1:1080 .
注意：此处可以将设置 listen-address 0.0.0.0:8118，这样局域网内也可以进行代理

注意：也可以使用另外一种方式配置，如: https://guojing.io/posts/privoxy/

配置/etc/profile
- 在末尾添加以下三行：
- export http_proxy=http://127.0.0.1:8118
- export https_proxy=http://127.0.0.1:8118
- export ftp_proxy=http://127.0.0.1:8118 #ftp的代理可以根据需要添加
注意： source /etc/profile

启动privoxy
sudo privoxy --user privoxy /etc/privoxy/config
注意：之后每次修改了配置文件后，都要执行sudo service privoxy restart来重启服务
