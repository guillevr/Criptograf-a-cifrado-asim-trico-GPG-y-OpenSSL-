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

Indicaremos nuestro nombre y apellidos y una direccion de correo.

### Generar clave en el equipo emisor
> guillevr@emisor:~$ gpg --gen-key
>
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.
> This is free software: you are free to change and redistribute it.
> There is NO WARRANTY, to the extent permitted by law.
>
> Nota: Usa "gpg --full-generate-key" para el diálogo completo de generación de clave.
>
> GnuPG debe construir un ID de usuario para identificar su clave.
>
> Nombre y apellidos: **Emisor Garcia Moreno**
> Dirección de correo electrónico: **emisor@gmail.com**
> Ha seleccionado este ID de usuario:
>     "Emisor Garcia Moreno <emisor@gmail.com>"

Si todo está correcto y no hay que modificar nada, introduciremos la letra **v**

> ¿Cambia (N)ombre, (D)irección o (V)ale/(S)alir? v

A continuación nos pedirá una contraseña de paso para proteger nuestra clave privada.

# Añadir IMAGEN FRASE DE PASO

> gpg: clave 0CC8CFD955118B0D marcada como de confianza absoluta
> gpg: creado el directorio '/home/guillevr/.gnupg/openpgp-revocs.d'
> gpg: certificado de revocación guardado como '/home/guillevr/.gnupg/openpgp-revocs.d/> DC435E571ECA4461419C43BA0CC8CFD955118B0D.rev'
> claves pública y secreta creadas y firmadas.
>
> pub   rsa3072 2021-11-30 [SC] [caduca: 2023-11-30]
>       DC435E571ECA4461419C43BA0CC8CFD955118B0D
> uid                      Emisor Garcia Moreno <emisor@gmail.com>
> sub   rsa3072 2021-11-30 [E] [caduca: 2023-11-30]

Nuestro par de claves se ha generado y añadido con confianza absoluta a nuestro keyring **pubring.kbx** (se encuentra almacenado en nuestro directorio personal, dentro de un directorio llamado .gnupg/). Además, ha generado de forma automática un certificado de revocación dentro de **.gnupg/openpgp-revocs.d/** por si nuestra clave privada llegase a malas manos o simplemente quisiésemos dejar de utilizar dicho par de claves, de manera que se notificará a otros usuarios que la clave pública no debe ser usada nunca más para cifrar.
