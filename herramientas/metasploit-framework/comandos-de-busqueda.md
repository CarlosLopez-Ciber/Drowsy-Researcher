# Metasploit - Comandos de Búsqueda

Metasploit Framework proporciona una potente funcionalidad de búsqueda (`search`) que permite localizar módulos específicos dentro de su extensa base de datos. Esta capacidad es fundamental para identificar rápidamente los _exploits_, _payloads_ o herramientas auxiliares más adecuados para una situación determinada. La búsqueda se realiza utilizando una serie de **parámetros de filtrado** que permiten refinar los resultados.

| Parámetro   | ¿Qué busca?                                                            | Ejemplo                   |
| ----------- | ---------------------------------------------------------------------- | ------------------------- |
| `name:`     | Busca por nombre de módulo                                             | `search name:apache`      |
| `type:`     | Busca por tipo de módulo (exploit, auxiliary, payload, post)           | `search type:exploit`     |
| `platform:` | Busca por plataforma (windows, linux, android, etc.)                   | `search platform:windows` |
| `arch:`     | Busca por arquitectura (x86, x64)                                      | `search arch:x64`         |
| `author:`   | Filtra por autor del módulo                                            | `search author:hdm`       |
| `cve:`      | Filtra por CVE específico                                              | `search cve:2020-1472`    |
| `edb:`      | Filtra por ID de Exploit-DB                                            | `search edb:12345`        |
| `ref:`      | Busca por referencias específicas (como MSB/MS advisories)             | `search ref:MS17-010`     |
| `date:`     | Busca por fecha de publicación (por año o más específico)              | `search date:2020`        |
| `rank:`     | Busca por ranking del exploit (excellent, good, normal, average, etc.) | `search rank:excellent`   |

**Ejemplo de búsqueda combinada**

```bash
msf > search type:exploit platform:windows cve:2017-0144
```

Este ejemplo buscaría **exploits** para **Windows** que estén relacionados con el famoso **CVE-2017-0144** (EternalBlue).

### <mark style="color:orange;">Consejos para búsquedas avanzadas:</mark>

* <mark style="color:yellow;">**Orden no importa**</mark><mark style="color:yellow;">:</mark> puedes poner los filtros en cualquier orden.
* <mark style="color:yellow;">**Cuantos más parámetros, más precisa**</mark> es la búsqueda.
* <mark style="color:yellow;">**Menos es más**</mark><mark style="color:yellow;">:</mark> empieza amplio y luego filtra más si ves demasiados resultados.
* <mark style="color:yellow;">**Usa**</mark><mark style="color:yellow;">**&#x20;**</mark><mark style="color:yellow;">**`info`**</mark><mark style="color:yellow;">**&#x20;**</mark><mark style="color:yellow;">**después**</mark><mark style="color:yellow;">:</mark> una vez encuentras algo interesante, usa `info <número o nombre>` para más detalles.
