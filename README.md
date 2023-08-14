# Glosario MongoDB

### Introducción a MongoDB

MongoDB es una base de datos NoSQL (No Structured Query Language) ampliamente utilizada en aplicaciones modernas para el almacenamiento y gestión de datos. A diferencia de las bases de datos relacionales tradicionales, MongoDB se basa en un modelo de almacenamiento orientado a documentos, lo que lo hace especialmente adecuado para manejar grandes cantidades de datos no estructurados o semi-estructurados

### ¿Qué es NoSQL?

NoSQL se refiere a tipos de bases de datos que no son relacionales, es decir, que no almacenan los datos en tablas con filas y columnas como las bases de datos SQL. NoSQL significa “no solo SQL” o “no SQL”, lo que indica que estas bases de datos pueden usar otros lenguajes o métodos para consultar los datos. Las bases de datos NoSQL se usan para manejar grandes volúmenes de datos no estructurados o semiestructurados.

### Tipos de bases de datos NoSQL:

##### Tipo Clave-Valor:

Este tipo de base de datos almacena la información con el modelo clave:valor. A través de la clave se puede recuperar el valor (dato). Los pares clave-valor se almacenan mediante una tabla hash.

##### Tipo Documento:

bases de datos de documentos amplían el concepto de la base de datos de pares clavevalor mediante la organización de documentos completos en grupos denominados colecciones. Admiten los pares clave-valor anidados y permiten realizar consultas de cualquier atributo dentro de un documento.

##### Tipo Columna:

Estas bases de datos almacenan información en columnas, lo que permite a los usuarios acceder solo a las columnas específicas que necesitan sin asignar memoria adicional a
datos irrelevantes.

##### **Tipo Grafo:**

Las bases de datos de grafos usan un modelo basado en nodos y bordes para representar datos interconectados, como las relaciones entre las personas en una red social, y ofrecen una navegación y un almacenamiento simplificados por las relaciones complejas.

## Ventajas:

* **Flexibilidad:** las NoSQL permiten almacenar variedad de formatos de datos, tanto estructurados como semiestructurados en un único almacén
* **Escalabilidad:** Alternativamente a escalar verticalmente agregando más servidores, las NoSQL pueden crecer horizontalmente utilizando hardware básico.
* **Alto Rendimiento:** Las NoSQL son especialmente valiosas cuando crecen los volúmenes de datos y de tráfico.
* **Disponibilidad:** Las NoSQL pueden replicar datos en múltiples servidores. Esto disminuye los
  tiempos de espera en los usuarios, sin importar su ubicación global

# ¿Qué es MongoDB?

MongoDB es una base de datos no relacional y de código abierto que utiliza documentos flexibles en lugar de tablas y filas para almacenar y procesar diferentes tipos de datos.

## Cómo funciona MongoDB

MongoDB es una base de datos orientada a documentos. Esto quiere decir que en lugar de guardar losdatos en registros, guarda los datos en documentos. Estos documentos son almacenados en BSON, que es una representación binaria de JSON.

**MongoDB: Ventajas y desventajas**

¿Sirve MongoDB para todo y todo? Antes de entrar a definir por qué usar MondoDB en tu proyecto,
conviene revisar pros y contras. MongoDB es un recurso muy interesante para desarrolladores pero no
es perfecto. Por ejemplo:

**Ventajas:**
-Validación de documentos
-Motores de almacenamiento integrado
-Menor tiempo de recuperación ante fallos

**Desventajas:**
-No es una solución adecuada para aplicaciones con transacciones complejas
-No tiene un reemplazo para las soluciones de herencia
-Aún es una tecnología joven comparada con las tecnologías SQL entre otras.

# Comandos más usados de Mongodb:

1. **Conexión y Gestión del Servidor:**
   * `mongod`: Iniciar el servidor MongoDB.
   * `mongo`: Conectar al servidor MongoDB y abrir la interfaz de línea de comandos de MongoDB.
   * `show dbs`: Mostrar la lista de bases de datos.
   * `use <database>`: Cambiar a una base de datos específica.
2. **Operaciones en Colecciones:**
   * `db.createCollection("nombre")`: Crear una nueva colección.
   * `db.<collection>.insert({})`: Insertar un nuevo documento en la colección.
   * `db.<collection>.find({})`: Realizar una consulta en la colección.
   * `db.<collection>.update({filtro}, {$set: {campo: valor}})`: Actualizar documentos en la colección.
   * `db.<collection>.remove({filtro})`: Eliminar documentos de la colección.
   * `db.<collection>.count()`: Contar la cantidad de documentos en la colección.
3. **Consultas y Operaciones:**
   * `db.<collection>.find({filtro}, {campos})`: Realizar una consulta con filtro y proyección de campos.
   * `db.<collection>.aggregate([pipeline])`: Realizar operaciones de agregación en la colección.
   * `db.<collection>.distinct("campo")`: Obtener valores únicos de un campo específico.
   * `db.<collection>.sort({campo: 1 o -1})`: Ordenar los resultados.
4. **Índices:**
   * `db.<collection>.createIndex({campo: 1 o -1})`: Crear un índice en un campo.
   * `db.<collection>.getIndexes()`: Obtener la lista de índices en la colección.
   * `db.<collection>.dropIndex({campo: 1 o -1})`: Eliminar un índice.
5. **Réplicas:**
   * `rs.initiate()`: Iniciar una configuración de réplica.
   * `rs.add("hostname:puerto")`: Agregar un miembro a la configuración de réplica.
   * `rs.status()`: Ver el estado de la configuración de réplica.
6. **Fragmentación (Sharding):**
   * `sh.enableSharding("base_de_datos")`: Habilitar fragmentación en una base de datos.
   * `sh.shardCollection("<base_de_datos>.<colección>", {campo_shard: 1 o "hashed"})`: Fragmentar una colección.
   * `sh.addShard("hostname:puerto")`: Agregar un servidor shard al clúster.
7. **Administración:**
   * `db.stats()`: Obtener estadísticas de la base de datos actual.
   * `db.shutdownServer()`: Apagar el servidor de MongoDB.


Para crear una colección con restricciones podemos seguir el siguiente codigo : 


use("db_limit_mongo");               //use la base de datos db_limit_mongo

db.createCollection("Cliente",{    //cree una coleccion llamada Cliente

    capped:true,

    size :690,               //tamaño maximo en bytes de la collección

    max :5,                    //Establece el número máximo de documentos que puede contener la colección.

    validator: {             //Define las validaciones para los documentos que se insertarán en la colección.

    $jsonSchema: {     //Permite especificar reglas y restricciones sobre la estructura y los valores de los documentos que se almacenan en una colección.

    bsonType:'object',  //los documentos deben ser objetos

    additionalProperties:false,  // Impide la adición de propiedades adicionales no especificadas en el esquema.

    required: ['ID_Cliente', 'nombre', 'DNI'], //Especifica las propiedades requeridas en cada documento: "cc", "nombre" y "edad".

    properties: {

    _id:{

    bsonType:'objectId',

    },

    ID_Cliente:{

    bsonType:"int", //tipo numerico

    description:"el ID_Cliente es obligatorio y tiene que se de tipo numerico"

    },

    nombre: {

    bsonType:'string',

    description:'{"status": "402", "message": "El nombre_usuario es obligatorio y solo resive letras"}' ,

    pattern:"^[a-zA-Z ]+$"//expresión regular para definir el valordel nombre

    },

    apellido: {

    bsonType:'string',

    description:'El apellido debe ser un string'

    },

    DNI: {

    bsonType:'int',

    description:'{"status": "402", "message": "El DNI es obligatorio y debe ser un numero"}'

    },

    }

    }

});


# Uso de AtlasDB:

MongoDB Atlas es un conjunto integrado de servicios de datos centrados en una base de datos en la nube diseñada para acelerar y simplificar la forma de construir con datos. Construya más rápido y de forma más inteligente con una plataforma de datos para desarrolladores que le ayuda a resolver sus retos de datos.

Para conectar Atlas con visual studio vamos a seguir los siguientes pasos:

1- descargamos la extension de visual  MongoDB (la de la hojita verde), seguido de ello seleccionamos Add MongoDB connection luego, oprimimos la opcion connect nos pedirá un link de conexión el cual encontraremos en la plataforma de Atlas:

link Atlas: En el costado derecho seleccionamos Database, luego connect,

![1691975145830](image/README/1691975145830.png)

 luego MongoDB for VS Code, en el punto 3, Connect to your MongoDB deployment, copia el link:

mongodb+srv:/`<nombreUsuario>`[:`<password>`@cluster0.vzylork.mongodb.net/](%E2%80%B8:%60%3Cpassword) 

cambia el nombre de usuario y la contraseña de tu plataforma.

agragas el link a la conexión de la extensión de mongo y te aparecerán todas las bases de datos que tengas.

![1691974993078](image/README/1691974993078.png)


# Conexión de Atlas con un proyecto:

1-Creamos una archivo .js con el siguiente codigo:

import dotenv from 'dotenv' //importamos dotenv para el manejo de variables de entorno en este caso variables de conexión

import { MongoClient } from'mongodb'; //libreria para interactuar con mongoDB

dotenv.config("../"); //configuracion de las variables de entorno

export async function con() { exportamos la variable de conexión en este caso la llamamos con()

  try {

    const uri=`mongodb+srv://${process.env.ATLAS_USER}:${process.env.ATLAS_PASSWORD}@cluster0.vzylork.mongodb.net/${process.env.ATLAS_DB}`; //debemos cambiar `vzylork` por el que nos genera el link de Atlas en la página

    const options= {

    useNewUrlParser:true,

    useUnifiedTopology:true,

    };

    const client=await MongoClient.connect(uri, options);

    return client.db();

  } catch (error) {

    return {status:500, message:error};

  }

}

2- Creamos un archivo .evn para almacenar las variables de entorno, en este caso las variables de conexión:

ATLAS_USER="Nombreusuario"

ATLAS_PASSWORD="contraseñas"

ATLAS_DB="nombreBaseDatos"

3-Ahora importamos la función con() del archivo del punto 1

import { con } from"../db/atlas.js"; //en este caso guardamos el archivo con el nombre atlas.js en una carpeta llamada db

4-Seguido de eso, creamos el siguiente codigo es un ejemplo de router con la petición Get: 


let db=await con(); //variable de conexión

let Alquiler=db.collection("Alquiler");

 appAlquiler.get("/todos", limitGrt(), appMiddlewareCampusVerify, async(req, res) => { //http://127.10.10.10:5011/Alquiler/todos

    if(!req.rateLimit) return;

    console.log(req.rateLimit);

    let db=awaitcon();

    let Alquiler=db.collection("Alquiler");

    let result=awaitAlquiler.find({}).toArray();

    res.send(result); });

export default appAlquiler;
