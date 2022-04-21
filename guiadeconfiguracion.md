# Configuracion de un CentOs contra un servidor de Active Directory

## Paginas consultadas 

[https://computingforgeeks.com/join-centos-rhel-system-to-active-directory-domain/](https://computingforgeeks.com/join-centos-rhel-system-to-active-directory-domain/)
[https://www.rootusers.com/how-to-join-centos-linux-to-an-active-directory-domain/](https://www.rootusers.com/how-to-join-centos-linux-to-an-active-directory-domain/)
[https://www.enmimaquinafunciona.com/pregunta/155700/sambakerberos-no-se-puede-contactar-con-ningun-kdc-kerberos-no-escucha](https://www.enmimaquinafunciona.com/pregunta/155700/sambakerberos-no-se-puede-contactar-con-ningun-kdc-kerberos-no-escucha
)

## Archivo de Configuracion /etc/krb5.conf
```
[libdefaults]
default_realm = PRUEBA.COM
      dns_lookup_kdc = no
      dns_lookup_realm = false
      default_keytab_name = /etc/krb5.keytab
      rdns=false

; for Windows 2003
      default_tgs_enctypes = rc4-hmac des-cbc-crc des-cbc-md5
      default_tkt_enctypes = rc4-hmac des-cbc-crc des-cbc-md5
      permitted_enctypes = rc4-hmac des-cbc-crc des-cbc-md5
udp_preference_limit = 0

; for Windows 2008 with AES
;      default_tgs_enctypes = aes256-cts-hmac-sha1-96 rc4-hmac des-cbc-crc des-cbc-md5
;      default_tkt_enctypes = aes256-cts-hmac-sha1-96 rc4-hmac des-cbc-crc des-cbc-md5
;      permitted_enctypes = aes256-cts-hmac-sha1-96 rc4-hmac des-cbc-crc des-cbc-md5
;
; for MIT/Heimdal kdc no need to restrict encryption type

[realms]
      PRUEBA.COM = {
              kdc = dc.prueba.com
              admin_server = dc.prueba.com
      }

[domain_realm]
      .linux.home = PRUEBA.COM
      .prueba.com = PRUEBA.COM
      prueba.com = PRUEBA.COM

[logging]
  kdc = FILE:/var/log/kdc.log
  admin_server = FILE:/var/log/kadmin.log
  default = FILE:/var/log/krb5lib.log
```