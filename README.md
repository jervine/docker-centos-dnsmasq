# docker-centos-dnsmasq
## dnsmasq daemon running on CentOS (7.4)
### Build Version: 4
Date of Build: 4th October 2017

The Dockerfile should intialise the CentOS image and subscribe to the EPEL repository.
The EPEL repository provides:

    supervisor

The dnsmasq daemon is controlled via the supervisord daemon which has a web front end exposed via port 9005. Default username and password for the web front end is admin:admin.

The dnsmasq package is installed from the standard CentOS repositories.

The container can be run as follows:

    docker pull jervine/docker-centos-dnsmasq
    docker run -d --network=<optional network> --name <optional container name> -h <optional hostname> -e TZ=<preferred timezone> -v /docker/config/dnsmasq/:/config -p 53:53 -p 53:53/udp jervine/docker-centos-dnsmas

The TZ variable allows the user to set the correct timezone for the container and should take the form "Europe/London". If no timezone is specified then UTC is used by default. The timezone is set up when the container is run. Subsequent stops and starts will not change the timezone.

The container can be verified on the host by using:

    docker logs <container id/container name>

Please note that the SELinux permissions of the config and downloads directories may need to be changed/corrected as necessary. [Currently chcon -Rt svirt_sandbox_file_t <directory>]
