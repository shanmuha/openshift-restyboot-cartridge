## Openshift Nginx Springboot Cartridge

A cartridge for OpenShift that enables OpenResty/NGINX to be used with spring boot. This OpenShift cartidge is not scalable yet.

This is based on multiple existing codebases.

### Installation

To install this cartridge you use the cartridge reflector from the command line. In the example below a "myapp" directory will be created in the location where the command is run as the git repo where your static web content will live will be cloned there.

	rhc create-app myapp http://cartreflect-claytondev.rhcloud.com/reflect?github=shanmuha/openshift-restyboot-cartridge


### Configuration

The cartridge installs two config files. One at <code>$OPENSHIFT_RESTYBOOT_DIR/conf/nginx.conf</code> which gets loaded by the executable
and sets up specific app configuration such as logs and pid files.

The config then includes another nginx.conf which must exist at <code>$OPENSHIFT_REPO_DIR/nginx.conf</code>. This config should
contain all your server specific set up including which ip/port to listen on.

The repo nginx.conf is actually seen in your repository as <code>nginx.conf.erb</code> so environment variables can be used
in the config. Every time the server starts it first processes <code>nginx.conf.erb</code>.


A <code>public/</code> folder is included where static content is served by default. However, as can be seen in the <code>nginx.conf.erb</code> file it
is entirely configurable and only exists as a form of documentation.
