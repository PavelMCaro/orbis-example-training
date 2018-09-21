# Eliminar archivo pesado en GIT

1. Se procedió a localizar donde se encuentra el archivo usando el comando **verify-pack**  y ordenando su salida por su tercera columna, la que nos informa de los tamaños de cada objeto. Ejecutamos el siguiente comando:

  **git verify-pack -v .git/objects/pack/pack-28b02e20378d605cb81e01bf20646b87966a9134.idx \ | sort -k 3 -n \ | tail -3**

2. Para concretar cual era el archivo, se utilizó el comando **rev-list**. Con la opción **--objects** obtendremos la lista de todas las SHA-1s de todas las confirmaciones de cambio, junto a las SHA-1s de los objetos binarios y las ubicaciones (paths) de cada uno de ellos. Usamos el siguiente comando para localizar el nombre del objeto binario:

  **git rev-list --objects --all | grep cfc3322ec593c88d0e4d68c312de3583ca741041**

3. Par aborrar el arhivo del historial de GIT empleamos el comando **filter-branch**. Utilizamos el siguiente comando:

  **git filter-branch --index-filter 'git rm --cached --ignore-unmatch sc.16.tar.gz' -- --all**

4. Ejecutamos los siguientes comandos para borrar los logs del git:

  **rm -rf .git/refs/original/**
  **rm -rf .git/logs**

7. Pasamos a empaquetar usando el garbage collection usando el siguiente comando:

  **git gc**

8. Procedimos a ejectuar el comando "**git count -objects -v**" para poder verificar que el archivo haya sido eliminado y el peso de la carpeta haya bajado.
