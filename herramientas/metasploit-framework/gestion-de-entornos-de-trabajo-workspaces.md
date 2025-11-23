# Gestión de Entornos de Trabajo (Workspaces)

Durante la ejecución de auditorías de seguridad o pruebas de penetración complejas, la segregación de datos es un requisito fundamentalPage 1 para mantener la integridad y organización del proyecto. Metasploit Framework integra una funcionalidad nativa denominada **Workspaces** (Espacios de Trabajo), diseñada para crear contenedores lógicos que aíslan la información de cada evaluación.

Un **workspace** funciona como una base de datos independiente que almacena todos los artefactos recolectados durante una auditoría: hosts, servicios, puertos abiertos, vulnerabilidades identificadas, credenciales obtenidas y sesiones activas. Su uso es una práctica estándar en entornos profesionales para evitar la contaminación cruzada de datos entre distintos objetivos o clientes.

***

## <mark style="color:green;">**Administración de Workspaces mediante Comandos**</mark>

La gestión de los espacios de trabajo se realiza a través del comando `workspace`, utilizando diferentes modificadores para realizar acciones específicas.

### <mark style="color:orange;">**1. Listado de Workspaces Disponibles**</mark>

Para visualizar todos los espacios de trabajo existentes, se ejecuta el comando `workspace` sin argumentos. El workspace activo se resalta con un asterisco (`*`).

* **Comando:** `workspace`
*   **Ejemplo de Salida:**

    ```
    msf6 > workspace
      default
    * pentest_cliente_a
      pentest_cliente_b
    ```

    En este caso, `pentest_cliente_a` es el contexto de trabajo actual.

### <mark style="color:orange;">**2. Creación de un Nuevo Workspace**</mark>

Para crear un nuevo entorno lógico, se utiliza el modificador `-a` (add) seguido del nombre deseado. Inmediatamente después de su creación, Metasploit cambia el contexto a este nuevo workspace.

* **Sintaxis:** `workspace -a <nombre_workspace>`
*   **Ejemplo :**

    ```
    msf6 > workspace -a red_corporativa
    [*] Added workspace 'red_corporativa'
    [*] Workspace: red_corporativa
    ```

    A partir de este momento, todos los datos, como la importación de un escaneo de Nmap (`db_import scan.xml`), se almacenarán exclusivamente en `red_corporativa`.

### <mark style="color:orange;">**3. Cambio del Contexto de Trabajo**</mark>

Para cambiar entre workspaces existentes, simplemente se ejecuta el comando `workspace` seguido del nombre del espacio de trabajo al que se desea cambiar.

* **Sintaxis:** `workspace <nombre_workspace>`
*   **Ejemplo :**

    ```
    msf6 > workspace default
    [*] Workspace: default
    ```

    Esta acción redirige todas las operaciones subsecuentes al workspace `default`, aislando el trabajo del entorno `red_corporativa`.

### <mark style="color:orange;">**4. Eliminación de un Workspace**</mark>

El modificador `-d` (delete) se utiliza para eliminar permanentemente un espacio de trabajo y toda la información que contiene.

> ⚠️ **Advertencia:** Esta operación es irreversible. Eliminar un workspace resultará en la pérdida de todos los hosts, servicios, credenciales y demás datos asociados a él. Se recomienda realizar una copia de seguridad (`db_export`) antes de proceder.

* **Sintaxis:** `workspace -d <nombre_workspace>`
*   **Ejemplo :**

    ```
    msf6 > workspace -d red_corporativa
    [*] Deleted workspace 'red_corporativa'
    [*] Switched back to workspace 'default'
    ```

***

### <mark style="color:orange;">**Flujo de Trabajo Operativo**</mark>

A continuación se muestra un escenario práctico que simula la gestión de dos evaluaciones de seguridad paralelas.

<mark style="color:yellow;">**Paso 1: Crear workspaces para dos clientes distintos.**</mark>

```
msf6 > workspace -a cliente_banco
[*] Added workspace 'cliente_banco'
[*] Workspace: cliente_banco

msf6 > workspace -a cliente_retail
[*] Added workspace 'cliente_retail'
[*] Workspace: cliente_retail
```

<mark style="color:yellow;">**Paso 2: Cambiar al contexto del primer cliente e importar datos.**</mark>

```
msf6 > workspace cliente_banco
[*] Workspace: cliente_banco

msf6 > db_import nmap_banco.xml
[*] Importing 'nmap_banco.xml'
...
msf6 > hosts
Hosts
=====
address       mac                name           os_name      os_flavor   os_sp  purpose  info  comments
-------       ---                ----           -------      ---------   -----  -------  ----  --------
192.168.1.10                      router.local   Linux        Ubuntu      18.04  server
192.168.1.15   0A:1B:2C:3D:4E:5F   ws01.local     Windows      10          Pro    client
```

<mark style="color:yellow;">**Paso 3: Cambiar al segundo cliente para verificar el aislamiento.**</mark>

```
msf6 > workspace cliente_retail
[*] Workspace: cliente_retail

msf6 > hosts
Hosts
=====
address  mac  name  os_name  os_flavor  os_sp  purpose  info  comments
-------  ---  ----  -------  ---------  -----  -------  ----  --------

```

Como se puede observar, la base de datos del workspace `cliente_retail` está vacía, demostrando la correcta segregación de los datos importados en el workspace `cliente_banco`.
