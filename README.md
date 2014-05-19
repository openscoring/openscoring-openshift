Openscoring application for the OpenShift cloud platform

# Prerequisites #

* OpenShift user account
* [OpenShift RHC Client tools] (https://www.openshift.com/developers/rhc-client-tools-install)

# Installation #

The Openscoring application embeds a Jetty web server. As such, it is suitable to be deployed as an OpenShift [DIY feature] (https://www.openshift.com/developers/do-it-yourself).

Create the application:
```
rhc app create <app name> diy-0.1 --from-code https://github.com/jpmml/openscoring-openshift.git
```

This command may take several minutes to execute, because the Openscoring application is built from scratch.

By default, the DIY cartridge initializes the Git repository with a dummy Ruby application. The option `--from-code` tells the DIY cartridge to replace that with the contents of the current repository.

# Usage #

The base URL of the application is `http://<app name>-<namespace name>.rhcloud.com`. The installation can be verified by making a GET request to the model list endpoint at `http://<app name>-<namespace name>.rhcloud.com/openscoring/model` (e.g. opening this address in a web browser). Upon success, the response should contain a JSON array of deployed model identifiers.

The application implements full [Openscoring REST API] (https://github.com/jpmml/openscoring).

# License #

Openscoring is dual-licensed under the [GNU Affero General Public License (AGPL) version 3.0] (http://www.gnu.org/licenses/agpl-3.0.html) and a commercial license.

# Additional information #

Please contact [info@openscoring.io] (mailto:info@openscoring.io)