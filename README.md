# Criptografía: cifrado asimétrico (GPG y OpenSSL)

## ¿Qué es la criptografía asimétrica?
La criptografía asimétrica (o criptografía de llave pública) permite establecer una conexión segura entre dos partes, autentificando mutuamente a las partes y permitiendo el traspaso de información entre los dos.

El sistema utiliza dos llaves para cifrar un mensaje: una llave pública y otra privada. Para encriptar un mensaje, se utiliza la llave pública del receptor (que se conoce a priori) y la privada del emisor. Para desencriptarlo se utiliza la llave pública del emisor (que se envía junto al mensaje cifrado) y la llave privada del receptor. La llave privada es secreta y es la única que permite descifrar los mensajes.

La objetivo es que nadie pueda descifrar la información en caso de que lograse interceptar el mensaje.

Estas llaves son generadas por cada usuario y son únicas. Incluso si se generan a partir de los mismos datos, las claves serán distintas.


## Generación de claves con GPG
Lo primero que debemos de hacer es crear un par de claves: una pública 
