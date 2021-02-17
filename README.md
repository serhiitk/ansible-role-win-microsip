# Ansible Role: Windows MicroSIP
An Ansible Role that installs, configures or uninstalls MicroSIP on Windows hosts.

## Requirements
Requires `WinRM` to be installed on the server (see https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html).

## Role Variables
Available variables are listed below, along with default values (see `defaults/main.yml`):

    drive_letter: 'C:'

The local Disk drive at which the Ansible's work dir and application MicroSIP will be installed.

    microsip_url: 'https://www.microsip.org/download'
    microsip_portable: 'MicroSIP-Lite-3.20.3.zip'

The URL and a portable version for MicroSIP installation.

    microsip_app_dir: '{{ drive_letter }}\Program Files\MicroSIP'

The location at which the MicroSIP application will be installed.

    psexec_url: 'https://download.sysinternals.com/files/PSTools.zip'

The URL to download PSTools.

    microsip_firewall_rules:
      - name: 'MicroSIP (TCP-In)'
        profiles: 'domain,private,public'
        protocol: 'TCP'
      - name: 'MicroSIP (UDP-In)'
        profiles: 'domain,private,public'
        protocol: 'UDP'

Default Firewall rules settings.

    microsip_regedit_data: '"{{ microsip_app_dir }}\{{ microsip_app_exe }}"'
    
    # For starting minimized use this:
    # microsip_regedit_data: '"{{ microsip_app_dir }}\{{ microsip_app_exe }}" /minimized'

Default Registry entry settings for run MicroSIP at system startup. 
If you need to start application minimized, you can override `microsip_regedit_data` as a commented example.

    microsip_settings_mainW:
    microsip_settings_mainH:
    
Sets default application window size.     
    
    accounts_default_server:
    accounts_default_domain:
    accounts_default_displayName:
    microsip_accounts:
      - label:
        server:
        domain:
        username:
        password:
        displayName:

MicroSIP accounts settings.

## Dependencies
None.



## Example Playbook

```yaml
- hosts: callcenter  

  roles:
    - role: win-microsip
```

## Examples of using Tags to debugging and uninstalling

### Example playbook name `contact_center.yml`

#### Ping hosts

    $ ansible-playbook contact_center.yml --tags 'ping'

#### Show generated template

    $ ansible-playbook contact_center.yml --tags 'show_template'

#### Get whoami information

    $ ansible-playbook contact_center.yml --tags 'whoami'

#### Uninstall MicroSIP

    $ ansible-playbook contact_center.yml --tags 'uninstall'
