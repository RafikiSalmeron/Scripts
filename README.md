# Ejercicios-scripts-Linux

## Ejercicio 1
### Elimina un archivo o directorio pasado como parámetro, y le pregunte si está seguro de llevar a cabo la acción.

```
#! /bin/bash

#Elimina un archivo o directorio pasado como parámetro, y le pregunte si está seguro de llevar a cabo la acción.

if [ -e $1]; then
	read -p "Quiere borrar el archivo o directorio (y/n)" op
	if [ "$op" = "y"] || [ "$op" = Y]; then
		rm -rf $1
		exit 0
	else
		exit 1
	fi
else
	echo "El archivo o directorio no existe"
fi
exit

```

## Ejercicio 2
### Muestra la información de un comando al ejecutar dicho script y pasar como parámetro el comando.


```
#!/bin/bash

#Muestra la información de un comando al ejecutar dicho script y pasar como parámetro el comando.

if [ $# -lt 1 ]; then
 	echo "No ha introducido ningun parametro"
 	exit 1
else
	man $1
fi
exit

```

## Ejercicio 3
### Comprueba si el usuario actual del sistema es blas, si es así visualiza su nombre 5 veces, sino te despides de él amigablemente.


```
#!/bin/bash

#Comprueba si el usuario actual del sistema es blas, si es así visualiza su nombre 5 veces, sino te despides de él amigablemente.

usuario=`whoami`

if [ $usuario == 'blas' ]; then
 	for i in {0..4}
 	do
 		echo "Hola Blas"
 	done
 	exit 0
else
	echo "Adios amigo, avisa a Blas"
fi
exit
```

## Ejercicio 4
### Muestra si la palabra clave de un archivo es el parámetro pasado o no.


```
#!/bin/bash

#Muestra si la palabra clave de un archivo es el parámetro pasado o no.

leer=`cat ./fichero.txt`

if [ $leer == $1 ]; then
	echo "Es correcto"
else
	echo "Es incorrecto"
fi
exit

```

## Ejercicio 5
### Suma, resta o multiplica según le indiquemos en el menú.

```
#! /bin/bash

#Tenemos un menu principal:
#(1) Suma
#Lee dos números y los suma.
#(2) Resta
#Lee dos números y los resta.
#(3) Multiplicación
#Lee dos números y los multiplica.
#(4) Salir
#Termina el script.

echo "     MENÚ      "
echo "1: Sumar"
echo "2: Restar"
echo "3: Multiplicar"
echo "4: Salir"
x=1
until [ $x ==4 ]; do
	case $x in
	1)
		read -p "Introduce un numero" a
		read -p "introduce un numero" b
		echo $((a+b))
	2)
		read -p "Introduce un numero" a
		read -p "introduce un numero" b
		echo $((a-b))
	3)
		read -p "Introduce un numero" a
		read -p "introduce un numero" b
		echo $((a*b))
	4)
		exit 0
	esac
done
exit
```

## Ejercicio 6
### Pide la edad y nos dice si es mayor de edad o menor.
```
#Pide la edad y nos dice si es mayor de edad o menor.

#! /bin/bash

read -p "Introduce tu edad: " edad

if [ $edad -lt 18 ]; then
	echo "Menor de edad"

elif [ $edad -gt 17 ]; then
	echo "Mayor de edad"
fi
exit
```

## Ejercicio 7

### Recibe un nombre de fichero, verifica que existe y que es un fichero de lectura-escritura,lo convierte en ejecutable para el usuario y el grupo y muestra el estado final de los permisos.

```
#! /bin/bash

if [ -f $1 ]; then
	echo "Es un fichero"
	ls -l $1
    if [ -r $1 ];then
    echo "Permiso de lectura"
        if [ -w $1 ];then
        	echo "Permisos de escritura "
        	chmod ug+x $1
        	ls -l $1
        else
        	echo "No es un fichero"
        fi
    else
    	echo "No es un fichero"
    fi
else
	echo "El fichero no existe "
fi
exit
```

# Ejercicio 8
### Nos dice al pulsar una tecla si es una letra, numero o caracter especial.


```
#! /bin/bash
# Nos dice al pulsar una tecla si es una letra, numero o caracter especial.

read -p "Introduce el carácter " caracter
case $caracter in
	[a-z,A-Z])
		echo "Ha introducido una letra"
	;;
	[0-9])
		echo "Ha introducido un número"
	;;
	*)
		echo "Ha introducido un caracter especial"
	;;
esac
```

# Ejercicio 9
### Recibe varios parametros y nos dice cuantos de esos parametros son de directorios y cuantos son archivos.

```
#! /bin/bash
# Recibe varios parametros y nos dice cuantos de esos parametros son de directorios y cuantos son archivos.
cd=0
cf=0

for i in $@;
do
   if [ -d $i ]; then
		cd=$(($cd+1))
   elif [ -f $i ]; then
		cf=$(($cf+1))
   else
		echo "$i no es fichero ni directorio"
   fi
done

echo "Se han introducido $cd directorios y $cf ficheros"
echo "Parametros introducidos $#"

exit
```
# Ejercicio 10
### Mostramos menu, con productos para vender, luego nos pide que introduzcamos la opcion. luego mensaje que indica que introduzca moneda. Si ponemos precio exacto nos da mensaje, "Gracias buen provecho", si ponemos menos, nos diga falta. Si poner mas valor, nos indique el cambio con mensaje.

```
#! /bin/bash

echo " Tienda Online "
echo "1. Ratón 30 euros"
echo "2. Cargador 5 euros"
echo "3. Cascos 15 euros"

read -p "Introduzca opcion:" x
read -p " Introduzca dinero: " dinero

case $op in
	1)
		precio=30
	;;
	2)
		precio=5
	;;
	3)
		precio=15
	;;
	*)
		echo "Opcion incorrecta"
	;;
esac

while [ $dinero -lt $precio ];
do
	faltaDinero=$(($precio-$dinero))
	read -p " Faltan $faltaDinero euros" extra
	dinero = $(($dinero+$extra))
done

if [ $din -gt $precio ]; then
	cambio=$(($dinero - $precio))
	echo "Su cambio es $cambio euros"
	echo "Gracias por su compra"
fi
exit
```


# Ejercicio 11
### Nos pide introducir la ruta de un directorio por teclado y nos dice cuantos archivos y cuantos directorios hay dentro de ese directorio.
```
#! /bin/bash

read -p "Introduzca la ruta de el directorio :" directorio
until [ -d $directorio ]; do
	read -p "Introduzca la ruta del directorio :" directorio
done

contadorDir=0
contadorFichero=0

for x in `ls $directorio`; 
	do
            if [ -d $x ]; then
            	contadorDir=$(($contadorDir+1))
            elif [ -f $x ]; then
            	contadorFichero=$(($contadorFichero+1))
            fi
     done
echo "Hay $contadorDir directorios y $contadorFichero ficheros"
exit
```
# Ejercicio 12
### Introduce un número por parámetro y muestra su tabla de multiplicar
```
#! /bin/bash

echo "La tabla de multiplicar de $1 es: "
for (( indice=0; indice<11; indice++ ))
do
   resultado=`expr $1 \* $indice`
   echo "$1 x $indice = $resultado"
done
```

# Ejercicio 13
### Limpia todas las reglas, y da permiso a todas las conexiones.
```
#! /bin/bash

`iptables -F`
`iptables -I INPUT -j ACCEPT`
`iptables -I OUTPUT -j ACCEPT`

exit
```

# Ejercicio 14
### Limpia todas las reglas, y prohíba cualquier conexión.
```
#! /bin/bash

`iptables -F`
`iptables -I INPUT -j REJECT`
`iptables -I OUTPUT -j REJECT`

exit
```

# Ejercicio 15
### Tendrá 3 parámetros: red(ip), entrada-salida, aceptar-denegar. Dará estos permisos a iptables.
```
#! /bin/bash

`iptables -A $2 -p tcp -s $1 -j $3`

`service iptables restart`

exit
```
