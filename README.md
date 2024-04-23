## Домашнее задание: Настройка PXE сервера для автоматической установки

```
При выполнении задания использовался Vagrant 2.4.0, Ansible 2.16.5, VirtualBox 7.0.14
 
Файлы:
- Vagrantfile       сценарий развертывания и настройки VMs 
- ansible.cfg:      конфигурационный файл ansible
- hosts:            inventory
- provision.yml:    ansible playbook настройки PXE сервера,
                    установки по сети CentOS Stream 8

- disk-httpd.yml:   сценарий настройки дополнительного диска VM pxeserver
                    и настройки httpd
- pxeboot.conf:     /etc/httpd/conf.d/pxeboot.conf конфигурационный файл httpd 

- dhcp-tftp.yml:    сценарий настройки dhcp и tftp серверов
- dhcpd.conf:       /etc/dhcp/dhcpd.conf конфигурационный файл dhcpd
- default:          /var/lib/tftpboot/pxelinux.cfg/default файл меню загрузки              

В настройках VM pxeclient установлен графический контроллер VMSVGA, видеопамять 20 МБ
 
Скриншоты загрузки по сети и установки CentOS в каталоге scrins
