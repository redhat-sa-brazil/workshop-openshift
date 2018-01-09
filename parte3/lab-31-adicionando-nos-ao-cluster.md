## OpenShift Installation Lab {#_openshift_installation_lab}

### Downloading the Binary {#downloading-the-binary}

Red Hat periodically publishes binaries to GitHub, which you can download on the OpenShift Origin repository’s[Releases](https://github.com/openshift/origin/releases)page. These are Linux, Windows, or Mac OS X 64-bit binaries; note that the Mac and Windows versions are for the CLI only.

The release archives for Linux and Mac OS X contain the server binary`openshift`which is an all-in-one OpenShift Origin installation. The archives for all platforms include[the CLI](https://docs.openshift.org/latest/cli_reference/get_started_cli.html#cli-reference-get-started-cli)\(the`oc`command\) and the Kubernetes client \(the`kubectl`command\).

**Installing and Running an All-in-One Server**

1. Download the binary from the[Releases](https://github.com/openshift/origin/releases)page and untar it on your local system.

2. Add the directory you untarred the release into to your path:

   ```
   $ export PATH="$(pwd)":$PATH
   ```

3. Launch the server:

   ```
   $ sudo ./openshift start
   ```

   This command:

   * starts OpenShift Origin listening on all interfaces \(**0.0.0.0:8443**\),

   * starts the web console listening on all interfaces at`/console`\(**0.0.0.0:8443**\),

   * launches anetcdserver to store persistent data, and

   * launches the Kubernetes system components.

   The server runs in the foreground until you terminate the process.

   |  | This command requires`root`access to create services due to the need to modify`iptables`and mount volumes. |
   | :--- | :--- |

4. OpenShift Origin services are secured by TLS. In this path we generate a self-signed certificate on startup which must be accepted by your web browser or client. You must point`oc`and`curl`at the appropriate CA bundle and client key and certificate to connect to OpenShift Origin. Set the following environment variables:

   ```
   $ export KUBECONFIG="$(pwd)"/openshift.local.config/master/admin.kubeconfig
   $ export CURL_CA_BUNDLE="$(pwd)"/openshift.local.config/master/ca.crt
   $ sudo chmod +r "$(pwd)"/openshift.local.config/master/admin.kubeconfig
   ```

   |  | This is just for example purposes; in a production environment, developers would generate their own keys and not have access to the system keys. |
   | :--- | :--- |

**What’s Next?**

Now that you have OpenShift Origin successfully running in your environment,[try it out](https://docs.openshift.org/latest/getting_started/administrators.html#try-it-out)by walking through a sample application lifecycle.

##  {#try-it-out}

  


