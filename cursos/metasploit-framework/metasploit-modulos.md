# Metasploit - Módulos

Un **módulo** en Metasploit es una pieza de código independiente que ejecuta una tarea específica, como explotar una vulnerabilidad, generar un payload, recolectar información, etc.

| Tipos de Módulos | Descripción                                                                                 |
| ---------------- | ------------------------------------------------------------------------------------------- |
| **Exploits**     | Código que aprovecha vulnerabilidades específicas.                                          |
| **Payloads**     | Código que se ejecuta después de explotar una vulnerabilidad (ej: meterpreter, shells).     |
| **Auxiliary**    | Herramientas que ayudan en reconocimiento, escaneo, y ataque (sin explotar).                |
| **Post**         | Módulos usados después de la explotación para movimientos laterales o recolección de datos. |
| **Encoders**     | Obfuscadores de payloads para evadir antivirus.                                             |
| **Nops**         | Pequeños "no-operation instructions" que estabilizan los payloads.                          |
| **Evasion**      | Técnicas activas para **evadir antivirus y EDR**.                                           |

> **"Todo en Metasploit es un módulo. Cada módulo tiene un propósito específico."**
