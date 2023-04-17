# fundamentos-etl-python

## 1. Crear container en Docker

Una vez que tengas instalado Docker en tu computador, ejecuta este comando en tu terminal:

WSL 2, Linux o macOS

```sh
sudo docker run -d --name=postgres -p 5432:5432 -v postgres-volume:/var/lib/postgresql/data -e POSTGRES_PASSWORD=mysecretpass postgres
```

Windows

```sh
docker run -d --name=postgres -p 5432:5432 -v postgres-volume:/var/lib/postgresql/data -e POSTGRES_PASSWORD=mysecretpass postgres
```

Como podrás notar, en este comando se específico lo siguiente para la creación de la base de datos con Docker:

- **Nombre del container:** --name=postgres
- **Puerto a compartir con la máquina local:** -p 5432:5432
- **Volumen para el manejo de disco e información:** -v \* **postgres-volume:**/var/lib/postgresql/data
- **Password en PostgreSQL:** POSTGRES_PASSWORD=mysecretpass

## 2. Validar container creado

Una vez que hayas creado el container de Docker usa el comando docker ps en tu terminal. Podrás ver todos los contenedores que se encuentran en ejecución actualmente y una descripción.

Deberás ver la IMAGE postgres.

![etl01.png](https://static.platzi.com/media/user_upload/etl01-fa8b573b-2c2c-4fbe-be69-d5a11557c884.jpg)

## 3. Configurar DataSpell

Para conectarte a la base de datos usarás un software de administración de bases de datos. Existen varios que puedes utilizar. Para el seguimiento del curso te sugiero utilizar DataSpell o, en su defecto, DBeaver.

DataSpell es un IDE completo para ciencia de de datos donde, además de conectarte y hacer consultas a bases de datos, podrás ejecutar Jupyter Notebooks. ¡Todo en el mismo lugar! 💪🏽

⚠️🦫 En caso de que decidas usar DBeaver en lugar de DataSpell, utiliza tu entorno local de Jupyter Notebooks con Anaconda para la ejecución del código Python de las siguientes clases. 🐍

## Instalación de DataSpell

1. Para instalar DataSpell [ve a su sitio web aquí](https://www.jetbrains.com/dataspell/) y descarga la versión para tu sistema operativo.📥

2. Instálalo siguiendo las instrucciones que te aparezcan en el instalador.

⚠️ Cuando te solicite actualizar PATH Variable acepta marcando la opción que te indique. Esto es para evitar errores de ambientes en el futuro. En Windows se ve así:

![PATH.png](https://static.platzi.com/media/user_upload/PATH-ce98cf48-8f18-4984-a64d-124f3b41b807.jpg)
Al finalizar te pedirá reiniciar el computador:

![restar_dataspell.png](https://static.platzi.com/media/user_upload/restar_dataspell-1207f830-1533-48f8-8f4b-f7c55129d819.jpg)

4. Abre DataSpell ya que se haya instalado. Al hacer esto por primera vez te pedirá iniciar sesión. Elige la versión free trial registrando tu cuenta para ello.

5. Una vez que tengas tu cuenta configurada te pedirá elegir un intérprete de Python 🐍.

Previamente deberás tener instalado Anaconda en tu sistema operativo. Te recomiendo que crees un ambiente de Anaconda (Conda environment) único para el proyecto del curso. Llama al ambiente fundamentos-etl.

Elige el ambiente de Anaconda que usarás para el proyecto y presiona el botón **Launch DataSpell**.

6. Crea un nuevo Workspace en DataSpell. Presiona el botón File en la barra superior y luego elige la opción New Workspace Directory.
   new_workspace_directory.png
   Llama fundamentos-etl al workspace y presiona el botón azul Create.

![new_etl_workspace.png](https://static.platzi.com/media/user_upload/new_workspace_directory-bb3e8547-004d-4d78-a850-9356c826d561.jpg)

## 4. Conexión a la base de datos PostgreSQL

Sigue estos pasos para conectarte a la base de datos postgres desde DataSpell.

1. Abre DataSpell en tu computador.
2. Ve a la pestaña de Database y en ella da clic en el botón de signo de +.
   ![database_dataspell.png](https://static.platzi.com/media/user_upload/database_dataspell-3ba09552-40ab-4eb3-b16a-bc91e0774177.jpg)
3. Selecciona la opción de Data Source y dentro del menú desplegable elige la opción de PostgreSQL.
   ![workspace 3_2_2023 7_48_03 PM.png](https://static.platzi.com/media/user_upload/workspace%203_2_2023%207_48_03%20PM-7ac11954-fd62-40f1-9858-e68f8b9a85c2.jpg)
4. Introduce los datos siguientes en la conexión:
   - Name: local_postgres
   - Host: localhost
   - Port: 5432
   - User: postgres
   - Database: postgres
   - Url (opcional): jdbc:postgresql://localhost:5432/postgres
   - Password: mysecretpass

Da clic en el botón de Test Connection para probar la conexión. Puede que te solicite actualizar unos drivers, acéptalos. Una vez que indique que la conexión es exitosa, da clic en el botón OK.

6. Listo, ya tienes tu base de datos conectada en DataSpell.
   postgresdataspell.png

## 5. Cargar datos en la base de datos Postgres

Dentro de DataSpell, ya con la conexión a la base de datos previamente creada, ejecutarás el script postgres_public_trades.sql.

Descárgalo aquí de [Google Drive](https://drive.google.com/file/u/2/d/19U7l0kp3mEh8SYYG6BjoDp0kVPYWDsqI/view?usp=share_link). 📥

⚠️Este archivo pesa cerca de 500 MB, por lo que puede demorar su descarga. Contiene la creación de una tabla llamada trades y los insert de registros de la tabla.

⚠️Es posible que al intentar correr este script en DBeaver no sea posible por falta de memoria. Te sugerimos cortarlo en varias partes y cargar cada script independientemente.

Una vez descargado el archivo postgres_public_trades.sql sigue estos pasos para cargar los datos con DataSpell:

1. Da clic derecho sobre la base de datos de PostgreSQL.
   ![etl04.png](https://static.platzi.com/media/user_upload/etl04-f61ba3e4-db90-4ff8-818d-c32ea05abb90.jpg)
2. Posteriormente da clic en SQL Script y luego en Run SQL Scripts.
   ![dataspell_run_sql_script.png](https://static.platzi.com/media/user_upload/dataspell_run_sql_script-41f0e59a-2efa-4d96-b263-d9a588448ffc.jpg)
3. Ubica el script descargado dentro de tu computador y da clic en OK.
   ![etl06.png](https://static.platzi.com/media/user_upload/etl06-61fb09da-48b1-4f33-a933-c5f9fcea7314.jpg)
   ⚠️La creación de la tabla y la carga de datos puede demorar cerca de 15-20 minutos en DataSpell.
   ![script_sql_done.png](https://static.platzi.com/media/user_upload/script_sql_done-acd62a7f-1846-4541-b128-15a5c3268ab0.jpg)

## 6. Prueba la tabla trades

Una vez terminada la ejecución del script, consulta la tabla Trades ya cargada. Abre el editor de queries desde tu base de datos en DataSpell e ingresa la siguiente consulta:

```sql
SELECT * FROM trades;
```

![etl07.png](https://static.platzi.com/media/user_upload/etl07-365b9489-ca61-443e-9105-15ac1710a94a.jpg)
¡Listo! Ya tienes lo esencial para comenzar a extraer datos de una base de datos OLTP y correr tus notebooks de Python.
