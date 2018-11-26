# Ansible role `Pound`

An Ansible role for POUND. Specifically, the responsibilities of this role are to:
 - Loabalance traffic over webservers

## Requirements

 - Running webservers

## Role Variables


| Variable   | Default | Comments (type)  |
| :---       | :---    | :---             |
| `role_var` | -       | (scalar) PURPOSE |

## Dependencies

No dependencies.

### Install EPEL
```
yum install epel-release
yum install Pound
```

### Configure pound.cfg based on variables
```
echo "
ListenHTTP
    Address $IPLB
    Port $PORTLB
End

ListenHTTPS
    Address $IPLB
    Port    $PORTLB
    Cert    "/etc/pki/tls/certs/pound.pem"
End

Service
    BackEnd
        Address $IPWEB1
        Port    $PORTWEB1
    End

    BackEnd
        Address $IPWEBX
        Port    $PORTWEBX
    End
End
" >> /etc/pound.cfg

```
### Open http and https ports
```
firewall-cmd --add-service=http --permanent
firewall-cmd --add-service=https --permanent
```
### Restart services
```
systemctl restart Pound
systemctl restart firewalld
```

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.

Pull requests are also very welcome. The best way to submit a PR is by first creating a fork of this Github project, then creating a topic branch for the suggested change and pushing that branch to your own fork. Github can then easily create a PR based on that branch. Don't forget to add your name to the contributor list below!

## License

2-clause BSD license, see [LICENSE.md](LICENSE.md)

## Contributors

- [Jens Neirynck](https://github.com/JensNeirynck/) (maintainer)
- [Bert Van Vreckem](https://github.com/bertvv/)

