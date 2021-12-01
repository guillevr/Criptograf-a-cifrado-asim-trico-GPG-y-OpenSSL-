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

### Generar clave pública en el equipo emisor
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

Si todo está correcto y no hay que modificar nada, introduciremos la letra **v.**

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

### Listar las claves **públicas** que tenemos en nuestro almacen de claves del equipo emisor.

Para listar las claves **públicas** ejecutaremos el comando **gpg --list-key**.

> guillevr@emisor:~$ gpg --list-key
> gpg: comprobando base de datos de confianza
> gpg: marginals needed: 3  completes needed: 1  trust model: pgp
> gpg: nivel: 0  validez:   1  firmada:   0  confianza: 0-, 0q, 0n, 0m, 0f, 1u
> gpg: siguiente comprobación de base de datos de confianza el: 2023-11-30
> /home/guillevr/.gnupg/pubring.kbx
> ---------------------------------
> pub   rsa3072 2021-11-30 [SC] [caduca: 2023-11-30]
>       DC435E571ECA4461419C43BA0CC8CFD955118B0D
> uid        [  absoluta ] Emisor Garcia Moreno <emisor@gmail.com>
> sub   rsa3072 2021-11-30 [E] [caduca: 2023-11-30]

### Listar las claves **privadas** que tenemos en nuestro almacen de claves del equipo emisor.

Para listar las claves **privadas** ejecutaremos el comando **gpg --list-secret-key**.

> guillevr@emisor:~$ gpg --list-secret-key
> /home/guillevr/.gnupg/pubring.kbx
> ---------------------------------
> sec   rsa3072 2021-11-30 [SC] [caduca: 2023-11-30]
>       DC435E571ECA4461419C43BA0CC8CFD955118B0D
> uid        [  absoluta ] Emisor Garcia Moreno <emisor@gmail.com>
> ssb   rsa3072 2021-11-30 [E] [caduca: 2023-11-30]








**-----------------------------------------------------------------------------**
**---------------         FALTA POR HACER                 ---------------------**
**-----------------------------------------------------------------------------**

### Generar clave pública en el equipo receptor

Si todo está correcto y no hay que modificar nada, introduciremos la letra **v.**

A continuación nos pedirá una contraseña de paso para proteger nuestra clave privada.

# Añadir IMAGEN FRASE DE PASO


### Listar las claves **públicas** que tenemos en nuestro almacen de claves del equipo receptor.
Para listar las claves **públicas** ejecutaremos el comando **gpg --list-key**.

### Listar las claves **privadas** que tenemos en nuestro almacen de claves del equipo receptor.
Para listar las claves **privadas** ejecutaremos el comando **gpg --list-secret-key**.

**-----------------------------------------------------------------------------**
**-----------------------------------------------------------------------------**
**-----------------------------------------------------------------------------**


## ¿Que información vemos cuando listamos las claves públicas y privadas?

- Claves públicas:
    - **pub** (public primary key) -> Información sobre par de claves publicas maestro.
    - **uid** (unique identifier) -> Información sobre la identidad del usuario en concreto (user-ID)
    - **sub** (public sub-key) -> Información sobre par de claves publicas secundario.
- Claves privadas:
    - **sec** (secret primary key) -> Información sobre par de claves privadas maestro.
    - **uid** (unique identifier) -> Información sobre la identidad del usuario en concreto (user-ID)
    - **ssb** (secret sub-key) -> Información sobre par de claves privadas secundario.

En la criptografía asimétrica siempre trabajamos con pares de claves: una clave pública para encriptar/comprobar firmas y una clave privada (secreta) para desencriptar/firmar, respectivamente.

Cuando generamos un par de claves OpenPGP con GnuPG, por defecto se genera un par de claves primario (también conocido como master-key) y un par de claves secundario. El par de claves primario contiene uno o más user-IDs (nombre, apellidos, correo electrónico) y se usa para para firmar/comprobar firmas, siendo así una prueba de identidad.

Por ello, debe guardarse con la clave privada de nuestro par de claves maestro. Por otro lado, el par de claves secundario se encuentra firmado por dicho par de claves primario, lo que confirma que pertenece a dicho user-ID y se usa para encriptar/desencriptar.
