# Inicialización Correcta de Metasploit

Antes de utilizar el <mark style="color:yellow;">**Metasploit Framework**</mark>, es fundamental preparar correctamente los servicios de backend que permiten su funcionamiento óptimo. Entre estos, destacan:

* <mark style="color:orange;">**PostgreSQL**</mark><mark style="color:orange;">:</mark> Motor de base de datos relacional utilizado por Metasploit para almacenar hosts, servicios, exploits, sesiones, credenciales, etc.
* <mark style="color:orange;">**MSF Database (msfdb)**</mark><mark style="color:orange;">:</mark> Componente que actúa como intermediario entre Metasploit y PostgreSQL, proporcionando persistencia y funciones avanzadas como importación de resultados, integración con Nmap, entre otras.

## <mark style="color:yellow;">Paso 1: Iniciar el servicio de PostgreSQL</mark>

PostgreSQL es una base de datos relacional usada por Metasploit para registrar resultados, objetos y estados durante una sesión de pentesting.

#### Comando para iniciar:

```bash
sudo systemctl start postgresql
```

#### Verificar estado:

```bash
sudo systemctl status postgresql
```

**Salida esperada:**

```
Active: active (exited) […]
```

#### Detener el servicio (opcional):

```bash
sudo systemctl stop postgresql
```

> **Nota**: PostgreSQL debe estar activo antes de lanzar Metasploit. Si no lo está, la base de datos no podrá usarse y muchas funcionalidades del Framework quedarán inhabilitadas.

## <mark style="color:yellow;">Paso 2: Inicializar la base de datos de Metasploit</mark>

`msfdb` es un servicio que configura y vincula Metasploit con PostgreSQL, creando las tablas necesarias y habilitando funcionalidades como `db_nmap`, `db_import`, `hosts`, `services`, entre otros.

#### Inicializar msfdb (por primera vez):

```bash
sudo msfdb init
```

Esto configurará automáticamente el acceso, creará los esquemas necesarios y verificará que PostgreSQL esté corriendo.

#### Verificar estado:

```bash
msfdb status
```

**Salida esperada:**

```
Database Status: Connected
```

#### Detener msfdb (opcional):

```bash
sudo msfdb stop
```

> Si es la primera vez que ejecutas `msfdb`, es probable que esté inactivo. El comando `init` lo activará y configurará de forma automática.

## <mark style="color:yellow;">Paso 3: Iniciar Metasploit Framework</mark>

Una vez configurados PostgreSQL y msfdb, puedes ejecutar el **entorno interactivo** del Metasploit Framework a través de su consola.

#### Comando:

```bash
msfconsole
```

**Proceso de carga inicial:**

* Verificación de la base de datos
* Carga de módulos auxiliares, exploits, payloads y post módulos
* Mostrar banner de bienvenida (cambia en cada ejecución)

**Salida esperada (resumen):**

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

> Puedes cambiar el banner cuantas veces quieras con el comando:

```bash
banner
```
