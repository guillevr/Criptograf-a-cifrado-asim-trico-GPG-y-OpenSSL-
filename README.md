# Criptografía: cifrado asimétrico (GPG y OpenSSL)

## ¿Qué es la criptografía asimétrica?
La criptografía asimétrica (o criptografía de llave pública) permite establecer una conexión segura entre dos partes, autentificando mutuamente a las partes y permitiendo el traspaso de información entre los dos.

El sistema utiliza dos llaves para cifrar un mensaje: una llave pública y otra privada. Para encriptar un mensaje, se utiliza la llave pública del receptor y la privada del emisor. Para desencriptarlo se utiliza la llave pública del emisor (que se envía junto al mensaje cifrado) y la llave privada del receptor.

La llave privada es secreta y es la única que permite descifrar los mensajes.

El objetivo es que nadie pueda descifrar la información en caso de que el mensaje fuera interceptado.

Estas llaves son generadas por cada usuario y son únicas. Incluso si se generan a partir de los mismos datos, las claves serán distintas.

## Sobre el sistema de cifrado asimétrico
El principal problema con los sistemas de cifrado simétrico no está ligado a su seguridad, sino al intercambio de claves. Una vez que el remitente y el destinatario hayan intercambiado las claves pueden usarlas para comunicarse con seguridad, pero ¿qué canal de comunicación que sea seguro han usado para «comunicar» la clave entre ellos? Sería mucho más fácil para un atacante intentar interceptar una clave que probar las posibles combinaciones del espacio de claves. Otro problema es el número de claves que se necesitan. Si tenemos un número n de personas que necesitan comunicarse entre ellos, entonces se necesitan n(n-1)/2 claves para cada pareja de personas que tengan que comunicarse de modo privado. Esto puede funcionar con un grupo reducido de personas, pero sería imposible llevarlo a cabo con grupos más grandes.

Los sistemas de cifrado de clave pública se inventaron con el fin de evitar por completo el problema del intercambio de claves. Un sistema de cifrado de clave pública usa un par de claves para el envío de mensajes. Las dos claves pertenecen a la misma persona a la que se ha enviado el mensaje. Una clave es pública y se puede entregar a cualquier persona. La otra clave es privada y el propietario debe guardarla para que nadie tenga acceso a ella. El remitente usa la clave pública del destinatario para cifrar el mensaje, y una vez cifrado, sólo la clave privada del destinatario podrá descifrar este mensaje.

Este protocolo resuelve el problema del intercambio de claves, que es inherente a los sistemas de cifrado simétricos. No hay necesidad de que el remitente y el destinatario tengan que ponerse de acuerdo en una clave. Todo lo que se requiere es que, antes de iniciar la comunicación secreta, el remitente consiga una copia de la clave pública del destinatario. Es más, esa misma clave pública puede ser usada por cualquiera que desee comunicarse con su propietario. Por tanto, se necesitarán sólo n pares de claves por cada n personas que deseen comunicarse entre ellas.

Los sistemas de cifrado de clave pública se basan en funciones-trampa de un sólo sentido. Una función de un sólo sentido es aquélla cuya computación es fácil, mientras que invertir la función es extremadamente difícil. Por ejemplo, es fácil multiplicar dos múmeros primos juntos para sacar uno compuesto, pero es difícil factorizar uno compuesto en sus componentes primos. Una función-trampa de un sentido es algo parecido, pero tiene una trampa. Esto quiere decir que si se conociera alguna pieza de la información, sería fácil computar el inverso. Por ejemplo, si tenemos un número compuesto por dos factores primarios y conocemos uno de los factores, es fácil computar el segundo. Dado un cifrado de clave pública basado en factorización de números primos, la clave pública contiene un número compuesto de dos factores primos grandes, y el algoritmo de cifrado usa ese compuesto para cifrar el mensaje. El algoritmo para descifrar el mensaje requiere el conocimiento de los factores primos, para que el descifrado sea fácil si poseemos la clave privada que contiene uno de los factores, pero extremadamente difícil en caso contrario.

Como con los sistemas de cifrado simétricos buenos, con un buen sistema de cifrado de clave pública toda la seguridad descansa en la clave. Por lo tanto el tamaño de la clave es una medida del seguridad del sistema, pero no se puede comparar el tamaño del cifrado simétrico con el de un cifrado de clave pública para medir la seguridad. En un ataque de fuerza bruta sobre un cifrado simétrico con una clave de un tamaño de 80 bits, el atacante debe enumerar hasta 281-1 claves para encontrar la clave correcta. En un ataque de fuerza bruta sobre un cifrado de clave pública con un clave de un tamaño de 512 bits, el atacante debe factorizar un número compuesto codificado en 512 bits (hasta 155 dígitos decimales). La cantidad de trabajo para el atacante será diferente dependiendo del cifrado que esté atacando. Mientras 128 bits es suficiente para cifrados simétricos, dada la tecnología de factorización de hoy en día, se recomienda el uso de claves públicas de 1024 bits para la mayoría de los casos.

## Requisitos
Un equipo emisor que va a ser el que envie el mensaje encriptado y un equipo emisor, el cual va a recibir el mensaje y descifrarlo.

En cuanto a requisitos que deba de cumplir el equipo no hay.

## Cifrado asimétrico con GPG
### Generación de claves con GPG
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

Para listar las claves **públicas** ejecutaremos el comando **gpg --list-key.**

> guillevr@emisor:~$ gpg --list-key   
> /home/guillevr/.gnupg/pubring.kbx
>
> pub   rsa3072 2021-11-30 [SC] [caduca: 2023-11-30]
>      DC435E571ECA4461419C43BA0CC8CFD955118B0D
> uid        [  absoluta ] Emisor Garcia Moreno <emisor@gmail.com>
> sub   rsa3072 2021-11-30 [E] [caduca: 2023-11-30]

### Listar las claves **privadas** que tenemos en nuestro almacen de claves del equipo emisor.

Para listar las claves **privadas** ejecutaremos el comando **gpg --list-secret-key.**

> guillevr@emisor:~$ gpg --list-secret-key    
> /home/guillevr/.gnupg/pubring.kbx
>
> sec   rsa3072 2021-11-30 [SC] [caduca: 2023-11-30]
>       DC435E571ECA4461419C43BA0CC8CFD955118B0D
> uid        [  absoluta ] Emisor Garcia Moreno <emisor@gmail.com>
> ssb   rsa3072 2021-11-30 [E] [caduca: 2023-11-30]

### Generar clave pública en el equipo receptor

> guillevr@receptor:~$ gpg --gen-key
>
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.
> This is free software: you are free to change and redistribute it.
> There is NO WARRANTY, to the extent permitted by law.
>
> Nota: Usa "gpg --full-generate-key" para el diálogo completo de generación de clave.
>
> GnuPG debe construir un ID de usuario para identificar su clave.
>
> Nombre y apellidos: Receptor Rodriguez Jurado
> Dirección de correo electrónico: receptor@gmail.com
> Ha seleccionado este ID de usuario:
>     "Receptor Rodriguez Jurado <receptor@gmail.com>"

Si todo está correcto y no hay que modificar nada, introduciremos la letra **v.**

> ¿Cambia (N)ombre, (D)irección o (V)ale/(S)alir? v

A continuación nos pedirá una contraseña de paso para proteger nuestra clave privada.

# Añadir IMAGEN FRASE DE PASO

>gpg: clave A5527020648689DB marcada como de confianza absoluta
>gpg: creado el directorio '/home/guillevr/.gnupg/openpgp-revocs.d'
>gpg: certificado de revocación guardado como '/home/guillevr/.gnupg/openpgp->revocs.d/05C7907B5CA1BF28CB3A9F27A5527020648689DB.rev'
>claves pública y secreta creadas y firmadas.
>
> pub   rsa3072 2021-12-02 [SC] [caduca: 2023-12-02]
>       05C7907B5CA1BF28CB3A9F27A5527020648689DB
> uid                      Receptor Rodriguez Jurado <receptor@gmail.com>
> sub   rsa3072 2021-12-02 [E] [caduca: 2023-12-02]

### Listar las claves **públicas** que tenemos en nuestro almacen de claves del equipo receptor.
Para listar las claves **públicas** ejecutaremos el comando **gpg --list-key**.

> guillevr@receptor:~$ gpg --list-key
> gpg: comprobando base de datos de confianza
> gpg: marginals needed: 3  completes needed: 1  trust model: pgp
> gpg: nivel: 0  validez:   1  firmada:   0  confianza: 0-, 0q, 0n, 0m, 0f, 1u
> gpg: siguiente comprobación de base de datos de confianza el: 2023-12-02
> /home/guillevr/.gnupg/pubring.kbx
>
> pub   rsa3072 2021-12-02 [SC] [caduca: 2023-12-02]
>       05C7907B5CA1BF28CB3A9F27A5527020648689DB
> uid        [  absoluta ] Receptor Rodriguez Jurado <receptor@gmail.com>
> sub   rsa3072 2021-12-02 [E] [caduca: 2023-12-02]


### Listar las claves **privadas** que tenemos en nuestro almacen de claves del equipo receptor.
Para listar las claves **privadas** ejecutaremos el comando **gpg --list-secret-key**.

> guillevr@receptor:~$ gpg --list-secret-key
> /home/guillevr/.gnupg/pubring.kbx
>
> sec   rsa3072 2021-12-02 [SC] [caduca: 2023-12-02]
>       05C7907B5CA1BF28CB3A9F27A5527020648689DB
> uid        [  absoluta ] Receptor Rodriguez Jurado <receptor@gmail.com>
> ssb   rsa3072 2021-12-02 [E] [caduca: 2023-12-02]


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

## Exportar la clave pública de Emisor y Receptor y realizar el intercambio

Primero, nos vamos al equipo Emisor y exportamos la clave publica con la siguiente orden: **gpg --export -a "nombre_apellidos_usuario" > nombre_fichero.key**.

> guillevr@emisor:~$ gpg --export -a "Emisor Garcia Moreno" > pk_emisorgm.key

Exactamente repetiremos el mismo paso pero en el equipo Receptor.

> guillevr@receptor:~$ gpg --export -a "Receptor Rodriguez Jurado" > pk_receptorrj.key

Lo siguiente que haremos será intercambiar las claves:

Enviamos la fichero con scp por ssh desde el Emisor al Receptor
> guillevr@emisor:~$ scp pk_emisorgm.key guillevr@10.0.2.8:~    
> guillevr@10.0.2.8's password:    
> pk_emisorgm.key                                                  100% 2464     2.1MB/s   00:00    
> guillevr@emisor:~$

Comprobamos en el equipo Receptor que tenemos el fichero correctamente.

> guillevr@receptor:~$ ls -l | grep "pk"   
> -rw-rw-r-- 1 guillevr guillevr 2464 dic  3 00:26 **pk_emisorgm.key**    
> -rw-rw-r-- 1 guillevr guillevr 2472 dic  3 00:24 pk_receptorrj.key    


Enviamos la fichero con scp por ssh desde el Receptor al Emisor

> guillevr@receptor:~$ scp pk_receptorrj.key guillevr@10.0.2.7:~  
> guillevr@10.0.2.7's password:   
> pk_receptorrj.key                                   100% 2472   866.6KB/s   00:00

Comprobamos en el equipo Emisor que tenemos el fichero correctamente.

> guillevr@emisor:~$ ls -l | grep "pk"     
> -rw-rw-r-- 1 guillevr guillevr 2464 dic  3 00:19 pk_emisorgm.key   
> -rw-rw-r-- 1 guillevr guillevr 2472 dic  3 00:33 **pk_receptorrj.key**   

## Importar claves publicas en los equipos

Para importar las claves del usuario Receptor en el equipo del usuario Emisor, ejecutaremos el comando **gpg --import <nombre_fichero>**.

> guillevr@emisor:~$ gpg --import pk_receptorrj.key    
> gpg: clave A5527020648689DB: clave pública "Receptor Rodriguez Jurado <receptor@gmail.com>" importada     
> gpg: Cantidad total procesada: 1    
> gpg:               importadas: 1
>

Posteriormente, comprobaremos que las claves de han incluido en nuestro almacen de claves:

> guillevr@emisor:~$ gpg --list-keys      
> /home/guillevr/.gnupg/pubring.kbx    
>
> pub   rsa3072 2021-11-30 [SC] [caduca: 2023-11-30]
>       DC435E571ECA4461419C43BA0CC8CFD955118B0D     
> uid        [  absoluta ] Emisor Garcia Moreno <emisor@gmail.com>     
> sub   rsa3072 2021-11-30 [E] [caduca: 2023-11-30]
>
> **pub   rsa3072 2021-12-02 [SC] [caduca: 2023-12-02]**
>       **05C7907B5CA1BF28CB3A9F27A5527020648689DB**      
> **uid        [desconocida] Receptor Rodriguez Jurado <receptor@gmail.com>**     
> **sub   rsa3072 2021-12-02 [E] [caduca: 2023-12-02]**

Ahora importaremos las claves del usuario Emisor en el equipo del usuario Receptor, ejecutaremos el comando **gpg --import <nombre_fichero>** al igual que en el anteriormente.

> guillevr@receptor:~$ gpg --import pk_emisorgm.key     
> gpg: clave 0CC8CFD955118B0D: clave pública "Emisor Garcia Moreno <emisor@gmail.com>" > importada    
> gpg: Cantidad total procesada: 1    
> gpg:               importadas: 1    


Posteriormente, comprobaremos que las claves de han incluido en nuestro almacen de claves:

> guillevr@receptor:~$ gpg --list-keys    
> /home/guillevr/.gnupg/pubring.kbx    
>
> pub   rsa3072 2021-12-02 [SC] [caduca: 2023-12-02]
>       05C7907B5CA1BF28CB3A9F27A5527020648689DB    
> uid        [  absoluta ] Receptor Rodriguez Jurado <receptor@gmail.com>    
> sub   rsa3072 2021-12-02 [E] [caduca: 2023-12-02]    
>
> **pub   rsa3072 2021-11-30 [SC] [caduca: 2023-11-30]**
>       **DC435E571ECA4461419C43BA0CC8CFD955118B0D**     
> **uid        [desconocida] Emisor Garcia Moreno <emisor@gmail.com>**   
> **sub   rsa3072 2021-11-30 [E] [caduca: 2023-11-30]**    


## Cifrar documentos

Lo siguiente que vamos a hacer es cifrar documentos. Para ello, me he descargado un fichero .pdf de internet, el cual, antes de cifrarlo, puedo ver el contenido perfectamente:

# CAPTURA PANTALLA SOBRE EL FICHERO PDF ABIERTO SIN PROBLEMAS

La sentencia del comando para cifrar es **gpg -e -u "emisor" -r "receptor" <fichero>**:

Donde:
- **-e (--encrypt)** -> cifra datos
- **-r (--recipient USER-ID)** -> cifra para ID-USUARIO (usuario receptor)
- **-u (--local-user USER-ID)** -> usa este identificador para firmar o descifrar (usuario emisor)

> guillevr@emisor:~$ gpg -e -u "Emisor Garcia Moreno" -r "Receptor Rodriguez Jurado" 2022_YZF1000R1SPL_es_ES.pdf      
> gpg: 091934B431AE0402: No hay seguridad de que esta clave pertenezca realmente al usuario que se nombra     
>
> sub  rsa3072/091934B431AE0402 2021-12-02 Receptor Rodriguez Jurado <receptor@gmail.com>     
>  Huella clave primaria: 05C7 907B 5CA1 BF28 CB3A  9F27 A552 7020 6486 89DB    
>       Huella de subclave: A057 0441 7DBF 5C34 D56D  7C9C 0919 34B4 31AE 0402    
>
> No es seguro que la clave pertenezca a la persona que se nombra en el identificador de usuario. Si *realmente* sabe lo que > está haciendo, puede contestar sí a la siguiente pregunta.    
>
> ¿Usar esta clave de todas formas? (s/N) **s**    

Como podremos comprobar, si listamos el directorio actual, comprobaremos que se ha creado un fichero con extension **.gpg**, el cual podemos abrir pero no podemos ver su contenido, ya que está cifrado:

> guillevr@emisor:~$ ls -l | grep "2022"    
> -rw-rw-r-- 1 guillevr guillevr 1141090 dic  3 17:51 2022_YZF1000R1SPL_es_ES.pdf     
> -rw-rw-r-- 1 guillevr guillevr  938092 dic  3 18:29 **2022_YZF1000R1SPL_es_ES.pdf.gpg**     


# CAPTURA PANTALLA DEL FICHERO NORMAL Y EL FICHERO CIFRADO
# CAPTURA PANTALLA DEL FICHERO ABIERTO DEL CUAL NO SE PUEDE VER EL CONTENIDO.

## Descifrar documentos

Enviamos el archivo cifrado del Emisor al equipo Receptor:

> guillevr@emisor:~$ scp 2022_YZF1000R1SPL_es_ES.pdf.gpg  guillevr@10.0.2.8:~     
> guillevr@10.0.2.8's password:     
> 2022_YZF1000R1SPL_es_ES.pdf.gpg                                                   100%  916KB  32.5MB/s   00:00

Comprobamos que le haya llegado al Receptor el correo perfectamente:

> guillevr@receptor:~$ ls -l | grep "2022"    
> -rw-rw-r-- 1 guillevr guillevr 938093 dic  4 21:16 2022_YZF1000R1SPL_es_ES.pdf.gpg

Nos vamos al equipo Receptor e intentamos abrir el fichero sin descifrarlo:

# CAPTURA PANTALLA DEL FICHERO ABIERTO DEL CUAL NO SE PUEDE VER EL CONTENIDO.

Desde el equipo Receptor, descifraremos el fichero con el sentencia **gpg -d <nombre_fichero>** donde la opcion **-d** significa "descifrar / desencriptar":

> guillevr@receptor:~$ gpg -d 2022_YZF1000R1SPL_es_ES.pdf.gpg

Tras ejecutarlo, nos pedirá la contraseña que introdujimos anteriormente al crear la clave privada, la cual nos va a hacer falta para descifrar el fichero.

# AÑADIR CAPTURA DONDE PIDE LA CONTRASEÑA PARA Descifrar

Una vez desencriptado, ya podríamos ver el contenido si fuera texto plano, pero en mi caso, al ser un fichero pdf, debemos volver a ejecutar la sentencia anterior pero redirigiendo la salida a un fichero con extension **.pdf**.

> guillevr@receptor:~$ gpg -d 2022_YZF1000R1SPL_es_ES.pdf.gpg > fichero.pdf     
> gpg: cifrado con clave de 3072 bits RSA, ID 091934B431AE0402, creada el 2021-12-02     
>       "Receptor Rodriguez Jurado <receptor@gmail.com>"

Ahora, comprobamos que podemos ver el contenido del fichero correctamente. Nos vamos a la carpeta donde esté el fichero y lo abrimos para ver el contenido:

# Añadir captura donde se encuentra el fichero desencriptado y donde se puede comprobar que abre perfectamente para ver su contenido.


## Eliminar claves publicas y privadas

Para eliminar las claves privadas del equipo ejecutaremos la sentencia **gpg --delete-secret-key "Nombre y apellidos del usuario local"** y para eliminar la clave publica, ejecutaremos la sentencia **gpg --delete-key "Nombre y apellidos del usuario"**

### Eliminar clave privada y publica del equipo Emisor

> guillevr@emisor:~$ gpg --delete-secret-key "Emisor Garcia Moreno"     
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.     
> This is free software: you are free to change and redistribute it.     
> There is NO WARRANTY, to the extent permitted by law.     
>
> sec  rsa3072/0CC8CFD955118B0D 2021-11-30 Emisor Garcia Moreno <emisor@gmail.com>     
>
> ¿Eliminar esta clave del anillo? (s/N) s     
> ¡Es una clave secreta! ¿Eliminar realmente? (s/N) s     
> guillevr@emisor:~$
> guillevr@emisor:~$ gpg --delete-key "Emisor Garcia Moreno"     
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.     
> This is free software: you are free to change and redistribute it.     
> There is NO WARRANTY, to the extent permitted by law.     
>
>
> pub  rsa3072/0CC8CFD955118B0D 2021-11-30 Emisor Garcia Moreno <emisor@gmail.com>     
>
> ¿Eliminar esta clave del anillo? (s/N) s    
> guillevr@emisor:~$    
> guillevr@emisor:~$ gpg --delete-key "Receptor Rodriguez Jurado"     
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.     
> This is free software: you are free to change and redistribute it.     
> There is NO WARRANTY, to the extent permitted by law.     
>
>
> pub  rsa3072/A5527020648689DB 2021-12-02 Receptor Rodriguez Jurado <receptor@gmail.com>     
>
> ¿Eliminar esta clave del anillo? (s/N) s   
> guillevr@emisor:~$       
> guillevr@emisor:~$ gpg --list-secret-key     
> gpg: comprobando base de datos de confianza     
> gpg: no se encuentran claves absolutamente fiables      
> guillevr@emisor:~$      
> guillevr@emisor:~$ gpg --list-key      
> guillevr@emisor:~$  




### Eliminar clave privada y publica del equipo Receptor

> guillevr@receptor:~$ gpg --delete-secret-key "Receptor Rodriguez Jurado"    
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.    
> This is free software: you are free to change and redistribute it.    
> There is NO WARRANTY, to the extent permitted by law.    
>
> sec  rsa3072/A5527020648689DB 2021-12-02 Receptor Rodriguez Jurado <receptor@gmail.com>    
>
> ¿Eliminar esta clave del anillo? (s/N) s    
> ¡Es una clave secreta! ¿Eliminar realmente? (s/N) s    
> guillevr@receptor:~$     
> guillevr@receptor:~$ gpg --delete-key "Emisor Garcia Moreno"    
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.    
> This is free software: you are free to change and redistribute it.    
> There is NO WARRANTY, to the extent permitted by law.    
>
>
> pub  rsa3072/A5527020648689DB 2021-12-02 Receptor Rodriguez Jurado <receptor@gmail.com>        
>
> ¿Eliminar esta clave del anillo? (s/N) s  
> guillevr@receptor:~$   
> guillevr@receptor:~$ gpg --delete-key "Emisor Garcia Moreno"    
> gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.    
> This is free software: you are free to change and redistribute it.    
> There is NO WARRANTY, to the extent permitted by law.    
>
>
> pub  rsa3072/0CC8CFD955118B0D 2021-11-30 Emisor Garcia Moreno <emisor@gmail.com>    
>
> ¿Eliminar esta clave del anillo? (s/N) s    
> guillevr@receptor:~$       
> guillevr@receptor:~$ gpg --list-secret-key     
> gpg: comprobando base de datos de confianza     
> gpg: no se encuentran claves absolutamente fiables      
> guillevr@receptor:~$      
> guillevr@receptor:~$ gpg --list-key      
> guillevr@receptor:~$  


## Cifrado asimétrico con OpenSSL
OpenSSL es un kit de herramientas de código abierto utilizado para implementar los protocolos Secure Sockets Layer (SSL) y Transport Layer Security (TLS). El kit de herramientas es de uso gratuito bajo la licencia OpenSSL y la licencia SSleay y está disponible para Windows, OS X y Linux.

El kit de herramientas OpenSSL es utilizado por muchos sistemas de código abierto, como las variantes de Linux, y la mayoría de los servidores web de Internet, como el servidor HTTP Apache. Los protocolos SSL y TLS, que implementa OpenSSL, permiten enviar información de forma segura a través de Internet cifrando los datos para que terceros no puedan acceder a la transmisión de datos.

También incluye una biblioteca criptográfica con implementaciones de cifrados simétricos, funciones hash, algoritmos de clave pública y otros algoritmos criptográficos.

## Generación de claves con OpenSSL

La sentencia del comando para cifrar es **openssl genrsa -aes128 -out <nombre_fichero.pem> 2048**:

Donde:
- **genrsa (Generation of RSA Private Key)** -> Genera clave privada
- **-aes128** -> Indicamos que la frase de paso que vamos a configurar utilice el algoritmo AES128.
- **-out** -> Fichero .pen donde queremos almacenar nuestras claves (crea un fichero unico).
- **2048** -> Indicamos el tamaño de la clave. (Lo recomentable es que sea de almenos 2048 bits).

### Generar clave pública en el equipo emisor

> guillevr@emisor:~$ sudo openssl genrsa -aes128 -out emisor.pem 2048    
> Generating RSA private key, 2048 bit long modulus (2 primes)    
> .....................+++++    
> ..+++++    
> e is 65537 (0x010001)    

Debemos de escribir dos veces la frase de paso (contraseña) para nuestro par de claves.

> Enter pass phrase for emisor.pem:     
> Verifying - Enter pass phrase for emisor.pem:     

Comprobaremos que se ha creado correctamente el fichero:

> guillevr@emisor:~$ ls -l | grep "emisor.pem"    
> -rw------- 1 root     root        1766 dic  6 22:00 emisor.pem    

### Generar clave pública en el equipo receptor

> guillevr@receptor:~$ sudo openssl genrsa -aes128 -out receptor.pem 2048    
> [sudo] contraseña para guillevr:     
> Generating RSA private key, 2048 bit long modulus (2 primes)    
> ...............................+++++    
> ......+++++    
> e is 65537 (0x010001)    

Debemos de escribir dos veces la frase de paso (contraseña) para nuestro par de claves.

> Enter pass phrase for receptor.pem:    
> Verifying - Enter pass phrase for receptor.pem:    

Comprobaremos que se ha creado correctamente el fichero:

> guillevr@receptor:~$ ls -l | grep "receptor.pem"     
> -rw------- 1 root     root        1766 dic  6 22:06 receptor.pem    

## Exportar la clave pública para enviarla

OpenSSl genera el par de claves (la clave publica y privada) en un mismo fichero, tendremos que extraer la clave publica para poder enviarla, ya que si envias el fichero que acabamos de generar, cualquiera podría descifrar los archivos/ficheros.

Para ello, ejecutaremos el comando **sudo openssl rsa -in <nombre_fichero.pem> -pubout -out <nombre_fichero.pem>**

Donde:
- **rsa** -> Indicamos el algoritmo que vamos a utilizar.
- **-in <nombre_fichero.pem>** -> Sirve para indicar el fichero donde se encuentra el par de claves.
- **-pubout** -> Indicamos que extraiga la clave pública del fichero.
- **-out <nombre_fichero.pem>** -> Indicamos donde queremos guardar la clave publica extraida.

Una vez hayamos ejecutado el comando, nos pedirá que introduzcamos la clave de paso creada anteriormente.

### Extraer la clave pública del equipo emisor

> guillevr@emisor:~$ sudo openssl rsa -in emisor.pem -pubout -out emisor_public.pem      
> [sudo] contraseña para guillevr:      
> Enter pass phrase for emisor.pem:     
> writing RSA key     

Comprobamos que se ha creado correctamente el fichero con la clave publica.

> guillevr@emisor:~$ ls -l | grep "emisor_public"          
> -rw-r--r-- 1 root     root         451 dic  6 22:17 emisor_public.pem         
> guillevr@emisor:~$      
> guillevr@emisor:~$ cat emisor_public.pem      
> -----BEGIN PUBLIC KEY-----     
> MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsVnsNMov5/oG5/RMEfgK     
> qtr+J/AqVfLle03yHNFN2LbAX6VQOmD81mag/0NV/VrjGLyU+m8/nOae7FpaBeJg     
> LFZni9cLC9LPPdSmGGeU2b8o6MZID9qIsxREhxXlI72mbI/OU8C1BgBk2+f3zmF0     
> dIcGiSnkzjOSq6ARY83GVLN2lGQS1Dk1Ts0XUlD424spf9hd7qlRxPbFs5yRILSa     
> Iiwv5+7lkd5v838fqDTXruVSGcmdZWpsNltSQV7NgcjEW+cUGl/pWa7Uu5I3PD+9     
> gxpwbwVdYH7Kvou/9I8Q0t9L11EfS/7ynvjq6JD90MYZCEACxnSPqEKDFM9C94FX     
> ewIDAQAB     
> -----END PUBLIC KEY-----     

### Extraer la clave publica del equipo receptor

> guillevr@receptor:~$ sudo openssl rsa -in receptor.pem -pubout -out receptor_public.pem     
> [sudo] contraseña para guillevr:     
> Enter pass phrase for receptor.pem:    
> writing RSA key    

Comprobamos que se ha creado correctamente el fichero con la clave publica.

> guillevr@receptor:~$ ls -l | grep "receptor_public"    
> -rw-r--r-- 1 root     root         451 dic  6 22:21 receptor_public.pem    
> guillevr@receptor:~$     
> guillevr@receptor:~$ cat receptor_public.pem     
> -----BEGIN PUBLIC KEY-----    
> MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA16950Q5kCEpF5pAKooD6    
> Tabv1TqC94nrxVOUmFL9PyxeSvbr9cFJgGuy9TNZGs8wNCpfGYSai+hnWvWEYdx3    
> /baN1N5B79Wtl6vxdE5siJsrf1+7ePCwIn5t0vCda+r35po9gSNUAx+oO0yTWnEJ    
> MLreXw3Tj+4VxYHN6GYDbnEtTMBvTJ/l0cln8uwDaiehKL3fvPZ3rGoctRSuH3FM    
> 5SxBRFwA2uqCSljT3kiuVGRnY+99CyRQBZ87B9Fb4Qfi9PdZJqHjlxIV6zKeiLgO    
> gvDCgnn8FnGu8ahjmB6mPvizM0HBDuspmzf04OAvIHqkTeYtjfA775IkCWj9zlyD    
> wwIDAQAB    
> -----END PUBLIC KEY-----    

### Intercambiamos las claves de los equipos

Enviamos la clave publica del Emisor al Receptor:

> guillevr@emisor:~$ scp emisor_public.pem guillevr@10.0.2.8:~     
> guillevr@10.0.2.8's password:      
> emisor_public.pem                                     100%  451   243.9KB/s   00:00       

Comprobamos en el equipo Receptor que la clave publica del Emisor ha llegado perfectamente:

> guillevr@receptor:~$ ls -l | grep "emisor"     
> -rw-r--r-- 1 guillevr guillevr     451 dic  6 22:26 emisor_public.pem     

Enviamos la clave publica del Receptor al Emisor:

> guillevr@receptor:~$ scp receptor_public.pem guillevr@10.0.2.7:~   
> guillevr@10.0.2.7's password:    
> receptor_public.pem                                      100%  451   187.7KB/s   00:00       

Comprobamos en el equipo Emisor que la clave publica del Receptor ha llegado perfectamente:

> guillevr@emisor:~$ ls -l | grep "receptor"     
> -rw-r--r-- 1 guillevr guillevr     451 dic  6 22:29 receptor_public.pem     
