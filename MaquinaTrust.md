# MAQUINA TRUST🕵🏻

Dificultad: Muy fácil

Website: [Dockerlabs](https://dockerlabs.es/)

----------------
## RECONOCIMIENTO.

Comenzamos realizando ping para probar que la maquina este en funcionamiento y que nos devuelva 1 paquete.

![image](https://github.com/user-attachments/assets/69ea66fb-5528-45f1-a896-c1cabf618c7a)

## ESCANEO DE PUERTOS.

Comenzamos realizando un escaneo general con **nmap** sobre la IP de la máquina víctima para ver que puertos tiene abiertos.

![image](https://github.com/user-attachments/assets/b55d013e-f75f-4774-8fd4-6ba9146c23aa)

Lanzamos un conjunto de scripts predeterminado con **nmap** para que nos reporte más información relacionada a los puertos descubiertos en el anterior escaneo, ademas de generarnos un archivo con la informacion obtenida, usando " -oX vulns ".

![image](https://github.com/user-attachments/assets/47b9921b-0b3a-4ac2-ac51-df4c9450b039)

El escaneo nos arrojara un archivo con la informacion obtenida del escaneo de la maquina, el cual convertiremos en HTML con la herramienta **xsltproc** para despues poder abrirlo y leerlo de una forma ordenada en el navegador.

![image](https://github.com/user-attachments/assets/d4d7dfb3-76e5-408f-877b-cad1cc07a22d)

Despues procederemos a abrir el archivo convertido, el cual estara ubicado en la carpeta donde estemos situados en nuestra shell al momento de hacer el escaneo con **Nmap**.

![image](https://github.com/user-attachments/assets/948201e1-2b58-453a-b58f-c70310af1ba2)
![image](https://github.com/user-attachments/assets/bfc17d14-b7bf-4ef1-a371-8f733f4aca76)

Haremos un nuevo escaneo con **NMAP** esta vez con los argumentos -sCV para ver si nos arroja algun escaneo diferente al anterior y convertir en **HTML** para poder leer mejor nuestro informe.

![image](https://github.com/user-attachments/assets/ceea823e-1971-47d1-abda-98b9b022ab49)
![image](https://github.com/user-attachments/assets/5f4d3f7e-3d0b-465b-bbbc-937c56e51f17)
![image](https://github.com/user-attachments/assets/a867ddfb-3366-40f1-846b-b9492caf5243)
![image](https://github.com/user-attachments/assets/83935730-5e5e-4362-afd8-b7399a64122e)

## ANALISIS DE VERSIONES Y VULNERABILIDADES.

Conociendo los puertos abiertos con el escaneo de **NMAP** sabemos que tenemos un puerto 22 y 80 abierto, el puerto 80 tiene un apache 2.4 segun nuestro informe de **NMAP**, mayormente albergan alguna pagina web, por lo cual probaremos con la IP en nuestro navegador a ver si conseguimos algo y revisaremos con wappalyzer a ver que otra informacion conseguimos.

![image](https://github.com/user-attachments/assets/a7e38398-e8b3-4e75-be69-49cf0d42e88d)

Al ver que no muestra ninguna pagina web de inicio, procederemos a escanear la pagina web con **dirbuster** para ver que otros enlaces puede tener esta IP.

![image](https://github.com/user-attachments/assets/f885d88a-6cef-493a-bc45-2c1e1be30986)

**Dirbuster** nos detecto un enlace interesante "/secret.php" el cual procederemos a abrir a ver que conseguimos.

![image](https://github.com/user-attachments/assets/0b24fdd1-70ce-4dec-98b4-b0b4e1dafacb)

## EXPLOTACION.

En la ultima imagen vemos que nos mostró una pagina web con un mensaje, un saludo a "mario", este posiblemente puede ser usuario de esta pagina, por lo cual guardaremos, revisamos el codigo fuente de la pagina web y no hay mas que el mensaje
por lo que procederemos a hacer un ataque de fuerza bruta al puerto 22 (ssh) con **Hydra**, conociendo un posible usuario "mario" podemos intentar conseguir la contraseña a ver si existe.

![image](https://github.com/user-attachments/assets/cca90abf-57ef-4571-b0bf-2516422e651e)
![image](https://github.com/user-attachments/assets/2887d894-b84a-47bc-a66c-9a3adecb564e)

Hemos encontrado una contraseña para el usuario "mario", por lo cual procederemos a conectarnos a la maquina a traves del puerto 22(ssh).

![image](https://github.com/user-attachments/assets/2765abe7-a4e1-42fd-9667-f6c6547934a0)

## ESCALACION DE PRIVILEGIOS.

Hemos logrado conectarnos a la maquina con el usuario y contraseña que forzamos con **Hydra**, pero al revisar pudimos ver que no es usuario "root", por lo que debemos intentar escalar privilegios para tener acceso total a la maquina.
al chequear los permisos de ejecucion, tenemos acceso a ejecutar "sudo -l", el cual nos dice que todos los usuarios (ALL) tienen acceso al binario (/usr/bin/vim) el cual pudieramos buscar en la Web **GTFObins** si existe alguna ejecucion para elevar privilegios con este binario.

![image](https://github.com/user-attachments/assets/cf6f29a8-b3ae-4559-9a6b-58df2f58599a)

Al revisar nos muestra que podemos ejecutar codigo para elevar privilegios a usuario "root", por lo cual procederemos a ejecutarlo, para elevar nuestros privilegios y concluir con la resolucion de esta maquina.

![image](https://github.com/user-attachments/assets/50112050-d81c-4c0b-9e10-31ecd44df319)












    


