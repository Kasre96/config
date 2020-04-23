# RabbitMQ
RabbitMQ is an open source message broker software that implements the Advanced Message Queuing Protocol (AMQP) and Streaming Text Oriented Messaging Protocol, 
Message Queuing Telemetry Transport, and other protocols via  Plugins.

# Installing RabbitMQ Server on Ubuntu 14.04 through 19.04
There are 2 ways to install RabbitMQ Server: 
- Using an apt repository on Package Cloud or Bintray (this option is highly recommended)
- Downloading the package and installing it manually with `dpkg -i`. This option will require manual installation of all package dependencies.

**NB**: RabbitMQ is included in standard Debian and Ubuntu repositories. However, the versions included are usually months or even years behind [latest RabbitMQ releases](https://www.rabbitmq.com/changelog.html), and thus are [out of support](https://www.rabbitmq.com/versions.html).

**NB**: Both method 1 & 2 require Erlang. We shall set it up

Reference: [Installing RabbitMQ on Debian and Ubuntu](https://www.rabbitmq.com/install-debian.html#apt-bintray-quick-start)

This is a guide for option 1 (using Bintray). For option 2, see [Manual Installation](https://www.rabbitmq.com/install-debian.html#manual-installation)

## 1. Add Repository Signing Key
In order to use the repository, add RabbitMQ signing key to `apt-key`. This will instruct apt to trust packages signed by that key.

`curl -fsSL https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc | sudo apt-key add -`

## 2. Enable apt HTTPS Transport
In order for apt to be able to download RabbitMQ and Erlang packages from Bintray, the `apt-transport-https` package must be installed:

`sudo apt-get install apt-transport-https`

## 3. Add a Source List File
As with all 3rd party Apt (Debian) repositories, a file describing the repository must be placed under the `/etc/apt/sources.list.d/` directory. `/etc/apt/sources.list.d/bintray.erlang.list` is the recommended location.

- `sudo nano /etc/apt/sources.list.d/bintray.erlang.list` (requires ano text-editor, or you can use one of your choice)
- Paste the following lines: 
  - `deb http://dl.bintray.com/rabbitmq-erlang/debian bionic erlang`
  - `deb https://dl.bintray.com/rabbitmq/debian bionic main`
  
**NB**: This will setup the latest versions for the bionic Ubuntu release. [See More](https://www.rabbitmq.com/install-debian.html#erlang-source-list-file)

## 4. Update Package indices
`sudo apt-get update -y`

## 4. Install rabbitmq-server and its dependencies
`sudo apt-get install rabbitmq-server -y --fix-missing`

## 5. Check status
`sudo systemctl status rabbitmq-server`

## 6. Enable the RabbitMQ management console so that you can monitor the RabbitMQ server processes from a web browser:
- `sudo rabbitmq-plugins enable rabbitmq_management`
- `sudo chown -R rabbitmq:rabbitmq /var/lib/rabbitmq/`

## 7. Set up admin user account[optional]
Next, you need to setup an administrator user account for accessing the RabbitMQ server management console. In the following commands, "mqadmin" is the administrator's username, "mqadminpassword" is the password. Remember to replace them with your own ones.
- `sudo rabbitmqctl add_user mqadmin mqadminpassword`
- `sudo rabbitmqctl set_user_tags mqadmin administrator`
- `sudo rabbitmqctl set_permissions -p / mqadmin ".*" ".*" ".*"`

## 8. Test on browser
`http://[your-server-IP]:15672/`
