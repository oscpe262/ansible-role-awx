# Ansible role 'ansible-role-awx'

An Ansible role for deploying AWX.

## Requirements
This role has been developed for CentOS7 and Fedora, but has the intention of being exandable with ease to cover other distros.

The role requires SELinux to be set to permissive, which is a lazy and crappy solution, but I haven't had the time or energy to sort it out. There are also some issues with EL7 lacking libselinux for python3 at the time of development, hence I've decided not to manage SELinux in this role for now. This might change down the line.

## Role Variables
All variables have set defaults, but it is recommended to use the vault file `vars/passwords.yml` to handle passwords, usernames etc.

| Variable		| Default		| Comments (type) |
| :---			| :---			| :---		  |
| `awx_repo` | `https://github.com/ansible/awx.git` | AWX git repo to clone |
| `awx_repo_dir` | `~/awx` | ...and where to clone it to. |
| `awx_version` | `devel` | Which branch to clone |
| `awx_keep_updated` |`true` | Update clone on run |

| `awx_postgres_server` | "" | If running postgres on a separate server, set this variable to the servers' fqdn |
| `awx_postgres_data_dir` | `var/lib/pgdocker` | Postgres path |
| `awx_pg_username` | `awx` | Postgres username |
| `awx_pg_password` | `awxpass` | Postgres password |
| `awx_pg_admin_password` | `postgrespass`| Postgres admin password |
| `awx_pg_database` | `awx` | Postgres database to use |
| `awx_pg_port` | `5432` | Port Postgres is served on |

| `awx_rabbitmq_password` | `awxpass` | Rabbitmq password |
| `awx_rabbitmq_erlang_cookie` | `cookiemonster` | Omnomnom |

| `awx_admin_user` | `admin` | Initial administrator user for AWX |
| `awx_admin_password` | `password` | ...and its password |

| `awx_preload_data` | `False` | Set to `True` if you wish demo data to be populated. This is the default for AWX. |
| `awx_secret_key` | `awxsecret` | This encryption key is used to keep data between upgrades. Set one and keep it. |
| `awx_project_data_dir` | `/var/lib/awx/projects` | AWX project data directory |

| `awx_proxy_url` | "" | URL to proxy if needed. Keep in mind that docker needs to be configured for that URL as well (not supported by this role)|
| `awx_noproxy` | "" | Domains for which the proxy shall not be used|

## Input as comma-separated lists.
| `awx_container_searchdomains` | "" | Search domains for the AWX container, provided as a comma-separated list as is. |
| `awx_alternate_dnsservers` | "" | If explicit DNS servers are needed, provide them as a comma-separated list.|

| `awx_ca_trust` | `false` | Set to `true` if you wish to use a CA-trust |
| `awx_ca_trust_dir` | `/etc/pki/ca-trust/source/anchors` | CA trust path |

| `awx_python_interpreter` | `python` | Which python interpreter that should be used. |

## Dependencies

## Example Playbook
```Yaml
- hosts: awx 
  roles:
    - role oscpe262.awx
```

## Testing


## License

MIT

## Contributors

Issues, feature requests, ideas, suggestions, etc. are appreciated and can be posted in the Issues section. Pull requests are also very welcome. Please create a topic branch for your proposed changes, it's the easiest way to merge back into the project.

- [Oscar Petersson](https://github.com/oscpe262/) (Maintainer)
