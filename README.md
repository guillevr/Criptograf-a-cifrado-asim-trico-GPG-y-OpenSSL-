# Criptografía: cifrado asimétrico (GPG y OpenSSL)

## ¿Qué es la criptografía asimétrica?
La criptografía asimétrica (o criptografía de llave pública) permite establecer una conexión segura entre dos partes, autentificando mutuamente a las partes y permitiendo el traspaso de información entre los dos.

El sistema utiliza dos llaves para cifrar un mensaje: una llave pública y otra privada. Para encriptar un mensaje, se utiliza la llave pública del receptor y la privada del emisor. Para desencriptarlo se utiliza la llave pública del emisor (que se envía junto al mensaje cifrado) y la llave privada del receptor.

La llave privada es secreta y es la única que permite descifrar los mensajes.

El objetivo es que nadie pueda descifrar la información en caso de que el mensaje fuera interceptado.

Estas llaves son generadas por cada usuario y son únicas. Incluso si se generan a partir de los mismos datos, las claves serán distintas.

## Requisitos
Un equipo emisor que va a ser el que envie el mensaje encriptado y un equipo emisor, el cual va a recibir el mensaje y descifrarlo.

En cuando a requisitos que deba de cumplir el equipo no hay.

## Generación de claves con GPG
Lo primero que debemos de hacer es crear un par de claves (una pública y una privada) en el equipo emisor y en el equipo receptor.

Para ello, ejecutaremos el comando **gpg --gen-key**.

### Equipo emisor
> guillevr@emisor:~$ gpg --gen-key
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.
> This is free software: you are free to change and redistribute it.
> There is NO WARRANTY, to the extent permitted by law.
> 
> Nota: Usa "gpg --full-generate-key" para el diálogo completo de generación de clave.
> 
> GnuPG debe construir un ID de usuario para identificar su clave.
> 
> Nombre y apellidos: 
