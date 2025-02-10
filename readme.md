To set this up, you need to supply your VMware (vCenter) details in the Image Builder configuration file. The exact file name and location may vary depending on your distribution and version, but it’s typically one of the following:

    /etc/osbuild-composer/composer.toml
    or /etc/osbuild-composer/config.toml

Example Configuration

Add (or update) a section for VMware in your configuration file. For example:

[vmware]
host = "vcenter.example.com"
username = "administrator@vsphere.local"
password = "YourVCenterPassword"
datacenter = "MyDatacenter"
datastore = "MyDatastore"
# Optional settings:
folder = "OVAFiles"         # (optional) Target folder on the datastore
port = 443                  # Defaults to 443 if omitted
validate_certs = false      # Set to false if using self-signed certificates

Steps to Enable Automatic Upload

    Edit the Configuration File:
    Open the configuration file (e.g., /etc/osbuild-composer/composer.toml) with your preferred text editor and add the [vmware] section with your vCenter details as shown above.

    Secure Your Credentials:
    Keep in mind that storing credentials in plain text is not ideal. In a production environment, consider integrating a secure secrets mechanism if possible.

    Restart the Image Builder Service:
    After modifying the configuration, restart the osbuild-composer service to load the new settings:

    sudo systemctl restart osbuild-composer

    Use the Cockpit UI:
    When you create a new image (compose) from a blueprint in Cockpit, you should see the “Upload to VMware” checkbox. With your configuration in place, checking this option will cause the OVA to be automatically uploaded to the specified vCenter datastore once the composition is finished.

    Monitor Logs if Needed:
    If you run into issues with the upload, check the osbuild-composer logs (typically found in /var/log/osbuild-composer/) for error messages or clues about what might be misconfigured.

Summary

    Configuration Location: Update /etc/osbuild-composer/composer.toml (or the applicable config file) with a [vmware] section.
    Parameters to Set: Provide your vCenter host, username, password, datacenter, datastore, and any optional parameters (like folder, port, or certificate validation settings).
    Activation: After a service restart, the “Upload to VMware” option in Cockpit will use these settings to automatically transfer the generated OVA once the image build is complete.
