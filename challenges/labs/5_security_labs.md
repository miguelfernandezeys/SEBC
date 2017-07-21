# Seguridad en CDH:
**Pilares de la seguridad en CDH y Cloudera Manager.**
* Autenticación: Los usuarios registrados pueden ser controlados a partir de integtración con Kerberos y directorio activo.
* Auditoria:Es posible la validación de logs de usuarios a partir de herramientas como Navigator.
* Confidencialidad:Se garantiza que la información transmitida en el cluster se mantenga oculta para usuarios o servidores ajenos a este.
* Autorización: Privilegios de acceso a recursos del Cloudera Manager y CDH, la autorización se ejecuta a partir del perfilamiento de usuarios mas permiso POSIX ACL y RABC.

* EN UN CLUSTER CON SEGURIDAD SOLO SE USA LA INTERFAZ DE RED ASOCIADA AL FQDN DE CADA NODO PARA TODO TRÁFICO RELACIONADO A HADDOP.
