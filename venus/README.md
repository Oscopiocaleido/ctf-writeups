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
