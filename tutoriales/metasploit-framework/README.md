---
icon: viruses
---

# Metasploit Framework

## <mark style="color:orange;">¿Qué es Metasploit Framework?</mark>

<mark style="color:yellow;">**Metasploit Framework**</mark> es una plataforma de código abierto diseñada para el desarrollo, prueba y ejecución de <mark style="color:yellow;">**exploits**</mark> contra sistemas remotos. Permite a **pentesters**, **red teamers** y **profesionales de seguridad** encontrar, validar y explotar vulnerabilidades de forma controlada.

### <mark style="color:green;">Terminología</mark>

#### <mark style="color:red;">Exploit</mark>

Un **exploit** es una técnica o programa que aprovecha una **vulnerabilidad** en un sistema, aplicación o servicio, con el objetivo de alterar su comportamiento normal.

> En otras palabras: un exploit es la **forma de ataque** que utiliza una debilidad para lograr algo que el sistema no debería permitir.

Ejemplos comunes de exploits incluyen:

* **Desbordamientos de búfer (buffer overflows)**
* **Vulnerabilidades en aplicaciones web** (como inyecciones SQL)
* **Errores de configuración**

#### <mark style="color:red;">Payload</mark>

El **payload** (carga útil) es el **código que queremos ejecutar en el sistema víctima** una vez que se ha explotado la vulnerabilidad.

> Es lo que ocurre _después_ de que el exploit ha tenido éxito.

* Un **reverse shell** es un payload que crea una conexión **desde la máquina víctima hacia el atacante**, permitiéndole controlar la consola remotamente.
* Un **bind shell** es un payload que "asocia" una consola de comandos a un **puerto en escucha** en la máquina víctima, al cual el atacante puede conectarse.

***

Piensa en un **exploit** como el **vehículo** que abre la puerta, y el **payload** como lo que introduces una vez abierta esa puerta.

***

## Índice

{% content-ref url="metasploit-modulos.md" %}
[metasploit-modulos.md](metasploit-modulos.md)
{% endcontent-ref %}
