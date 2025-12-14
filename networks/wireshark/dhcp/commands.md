## MikroTik

/ip dhcp-server print - показать список DHCP-серверов  
/ip dhcp-server disable dhcp1 - отключить DHCP-сервер dhcp1  
/ip address add address=172.16.10.1/24 interface=ether2 - назначить IP на интерфейс второй подсети  
/ip dhcp-relay add name=relay1 interface=ether2 dhcp-server=192.168.10.2 local-address=172.16.10.1 - создать DHCP Relay на MikroTik  
/ip dhcp-relay enable relay1 - включить DHCP Relay  

## Ubuntu (DHCP server isc-dhcp-server)

sudo apt install isc-dhcp-server -y - Устанавливаем DHCP-сервер

INTERFACESv4="ens3" - Указываем интерфейс для работы (редактируем /etc/default/isc-dhcp-server)

#### Настройка пула адресов (редактируем /etc/dhcp/dhcpd.conf)
`subnet 192.168.10.0 netmask 255.255.255.0 {
    range 192.168.10.10 192.168.10.99;
    option routers 192.168.10.1;
    option domain-name-servers 8.8.8.8;
    default-lease-time 86400;
    max-lease-time 86400;
}`

#### Добавление второй подсети для работы через DHCP Relay
`subnet 172.16.10.0 netmask 255.255.255.0 {
    range 172.16.10.10 172.16.10.99;
    option routers 172.16.10.1;
    option domain-name-servers 8.8.8.8;
    default-lease-time 86400;
    max-lease-time 86400;
}`

sudo dhcpd -t -cf /etc/dhcp/dhcpd.conf - Проверка конфигурации

sudo systemctl restart isc-dhcp-server - Запуск службы

## Windows (клиент)

/ipconfig /release - освободить текущий IP-адрес  
/ipconfig /renew - запросить новый IP-адрес  

## Клиент Linux (Ubuntu)

/sbin/dhclient - запустить DHCP-клиент для получения IP  

