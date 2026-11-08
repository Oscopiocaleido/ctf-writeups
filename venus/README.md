![Status](https://img.shields.io/badge/status-in%20progress-green)

**Plataforma:** HackMyVM  

**Dificultad:** principiante 

**Flags:** 50 (17 ocultas)

## Información general
- IP/Host: venus.hackmyvm.eu
- Fecha de inicio: 2026-11-04
- Estado: en progreso

## Reconocimiento inicial
El acceso inicial fue provisto por la plataforma mediante credenciales SSH 
(usuario `hacker`).

Al listar el directorio con `ls`, encontré dos archivos: `mission.txt` y 
`readme.txt`. 

## Misiones resueltas
### Misión 0x01: Acceder como Sophia
- Pista dada: La usuaria sophia ha guardado su contraseña en un fichero oculto en esta carpeta.Encuentralo y logueate como sophia.

- Técnica usada: Listé el contenido del directorio incluyendo archivos ocultos con `ls -a`, ya que los archivos que comienzan con `.` no aparecen en un listado normal. Esto reveló un fichero oculto con la contraseña de Sophia en texto plano. Leí su contenido con `cat` y usé esas credenciales para autenticarme como ella mediante `su sophia`. 

Una vez dentro de su sesión, volví al directorio superior con `cd ..` para acceder a la carpeta personal de Sophia, donde se encontraba la flag correspondiente.

- Por qué funciona: Almacenar contraseñas en texto plano es una mala práctica de seguridad, incluso 
si el archivo está "oculto" `ls -a` revela cualquier archivo que empiece con `.` 
a cualquier usuario con acceso al sistema de archivos. La ocultación por convención 
no es una medida de seguridad real.

- Flags obtenidas: flag [01]

### Misión 0x02: Encontrar el fichero whereismypazz.txt
- Pista dada: La usuaria Angela ha guardado su password en un fichero pero no recuerda donde... solo recuerda que el fichero se llamaba whereismypazz.txt

- Técnica usada: Para encontrar el fichero en todo el sistema utilicé `find`, comenzando desde la ruta `/` (todo el sistema) y con la bandera `-name [nombre]` indicando el nombre del archivo que es "whereismypazz.txt", luego el comando find lo que hace es recorrer todo el sistema buscando el nombre del archivo, ubicando el archivo en la ruta `/usr/share/`. Al final leí el contenido del archivo con `cat` y usé esas credenciales para acceder como Angela mediante `su angela`. 

Una vez dentro de la sesión de Angela, volví al directorio principal con `cd /` luego entré al directorio de Angela con `cd pwned/angela`, donde se encontraba la flag correspondiente.

- Por qué funciona: El archivo estaba ubicado en `/usr/share/`, un directorio del sistema destinado a recursos compartidos entre aplicaciones y, por tanto, legible por cualquier usuario. El problema de seguridad no es un permiso mal configurado, sino la ubicación: guardar credenciales en una ruta pensada para ser pública la expone a cualquier usuario del sistema que sepa (o adivine) el nombre del archivo, incluso usando herramientas como 
`find`.

- Flags obtenidas: flag [02]

### Misión 0x03: Encontrar la contraseña en la linea 4069

- Pista dada: La password de la usuaria emma esta en la linea 4069 del fichero findme.txt

- Técnica usada: Estando en la sesión de Angela (obtenida en la misión anterior), listé el contenido de su directorio con `ls` y encontré el archivo `findme.txt`. Para extraer la contraseña en la línea indicada por la pista, utilicé el comando `sed -n "4069p" findme.txt`, que imprime únicamente esa línea específica del archivo.Con la contraseña obtenida, accedí como Emma mediante `su emma`.

Una vez dentro de la sesión de Emma, me dirigí a `cd /home/emma`, donde se encontraba la flag correspondiente.

- Por qué funciona: El archivo `findme.txt` se encontraba en el directorio de Angela, a la que accedí en la misión anterior. Que un archivo con la contraseña de Emma residiera en el espacio de otro usuario es un problema de segregación: cada usuario debería tener acceso únicamente a sus propios datos sensibles, no a los de otros. 

- Flags obtenidas: flag [03]

### Misión 0x04: Encontrar el fichero -
- Pista dada: La usuaria mia ha dejado su password en el fichero -.

- Técnica usada: Utilicé el comando `ls -a` para listar todos los ficheros del directorio de la usaria Emma, como en dicho directorio estaba un fichero con nombre "-", tenemos el fichero que estabamos buscando, para asegurarme que era el único con dicho nombre usé `find / -name "-"` y arrojaba la ruta del directorio de Emma.

Accediendo como Mia con `su mia` y utilizando las credenciales obtenidas por el archivo "-", nos movemos a su directorio obteniendo la flag correspondiente a la misión.

- Por qué funciona: Como el caso anterior, que el archivo con la contraseña de Mia residiera en el espacio de otro usuario es un problema de segregación, cada usuario debería tener acceso únicamente a sus datos sensibles, no a los de otros.

- Flags obtenidas: flag [04]
