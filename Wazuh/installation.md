# Wazuh server/master node installation on ubuntu using apt

* [Wazuh installation guide](https://documentation.wazuh.com/current/installation-guide/wazuh-server/step-by-step.html) - Wazuh server/master node installation on ubuntu Documentation

## Switch normal user to root user
    sudo su

## Adding the Wazuh repository
    apt-get install -y gnupg apt-transport-https
    curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg
    echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
    apt-get -y update

### Installing the Wazuh manager and Filebeat

    apt-get -y install wazuh-manager
    apt-get -y install filebeat

