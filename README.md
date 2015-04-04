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

The base URL of the application is `http://<app name>-<namespace name>.rhcloud.com`. The installation can be verified by making a GET request to the model list endpoint at `http://<app name>-<namespace name>.rhcloud.com/openscoring/model` (e.g. opening this address in a web browser). Upon success, the response should contain a summary of deployed models as a JSON object.

The application implements full [Openscoring REST API] (https://github.com/jpmml/openscoring). The access to HTTP methods `PUT` and `DELETE` that deal with model deployment and undeployment, respectively, is only permitted to users with the "admin" role. The Openscoring application grants this role to all users that originate from the local network.

The Openscoring application watches the contents of the auto-deploy directory `pmml` for changes. A model can be deployed by placing a new PMML file into that directory. Conversely, a model can be undeployed by removing an existing PMML file from that directory. In both cases, the changes must be first committed to the local repository and then pushed to the remote repository.

Deploying a file `DecisionTreeIris.pmml`:
```
cp ~/work/DecisionTreeIris.pmml pmml/DecisionTreeIris.pmml
git add pmml/DecisionTreeIris.pmml
git commit -m "Added a model"
git push origin master
```

The name of the file (without file name extension(s), if any) becomes the model identifier. Hence, the newly deployed model can be reached at `http://<app name>-<namespace name>.rhcloud.com/openscoring/model/DecisionTreeIris`.

Undeploying a file `DecisionTreeIris.pmml`:
```
git rm pmml/DecisionTreeIris.pmml
git commit -m "Removed a model"
git push origin master
```

# License #

Openscoring is dual-licensed under the [GNU Affero General Public License (AGPL) version 3.0] (http://www.gnu.org/licenses/agpl-3.0.html) and a commercial license.

# Additional information #

Please contact [info@openscoring.io] (mailto:info@openscoring.io)