# 1. Describa que es un algoritmo

Un algoritmo es un conjunto de reglas y pasos bien definidos y ordenados que se utilizan para resolver un problema o realizar una tarea específica. Es como un plan o una receta que te ayuda a seguir los pasos necesarios para lograr un objetivo. Los algoritmos se utilizan en una variedad de campos, como la informática, la matemática y la ciencia, y pueden ser tan simples como una lista de instrucciones para cocinar una cena o tan complejos como un sistema de inteligencia artificial. En resumen, un algoritmo es una herramienta muy útil para resolver problemas y automatizar tareas.

#  2. Desarrolle un programa en cualquier lenguaje, que realice la siguiente operación:
a. Debe recibir dos valores numéricos, ‘inicio’ y ‘fin’. 
b. Debe recorrer todos los números desde ‘inicio’ a ‘fin’, siguiendo las reglas a continuación: 
i. Si el número en cuestión es divisible entre 2, debe escribir “pin”. 
ii. Si el número en cuestión es divisible entre 3, debe escribir “tin”. 
iii. Si el número en cuestión es divisible entre 5, debe escribir “fla”. 
c. El programa debe escribir sólo una opción por iteración, la mayor opción tiene prioridad.

    <?php  
    function imprimir_numeros($inicio, $fin) {
		for ($i = $inicio; $i <= $fin; $i++) { 
			if ($i % 5 == 0) { echo  "fla"; }
		    elseif ($i % 3 == 0) { echo  "tin"; }
		    elseif ($i % 2 == 0) { echo  "pin"; }
	     }
	} 
	imprimir_numeros(5, 15); 
	?>
    




## 3. Un usuario denominado “Jefe de Operaciones” puede realizar diversos tickets en un sistema “X”.
Estos tickets están relacionados a un edificio, el cual posee “n” cantidad de áreas en su interior. 
Sabiendo que existe un superusuario que clasifica y aprueba estas solicitudes, realice lo siguiente: 
a. Elabore el modelo Entidad- Relación correspondiente a la base de datos del enunciado. 
b. Indique la consulta para conocer los nombres y cargos de los usuarios. 
c. Indique las áreas de un edificio que posean tickets aprobados con código mayor a 1000.

> a. El modelo Entidad-Relación para la base de datos del enunciado
> podría ser el siguiente:
> 
> Entidad "Usuario":
> 
> -   Atributos: id (llave primaria), nombre, cargo, email, contraseña
> 
> Entidad "Edificio":
> 
> -   Atributos: id (llave primaria), nombre, dirección, cantidad de áreas
> 
> Entidad "Área":
> 
> -   Atributos: id (llave primaria), nombre, descripción, id_edificio (llave foránea hacia Edificio)
> 
> Entidad "Ticket":
> 
> -   Atributos: id (llave primaria), descripción, fecha_creación, estado, id_usuario (llave foránea hacia Usuario), id_area (llave
> foránea hacia Área)
## 
> b. La consulta para conocer los nombres y cargos de los usuarios
> podría ser la siguiente:
> 
>     `SELECT nombre, cargo FROM Usuario;`
## 
> c. La consulta para conocer las áreas de un edificio que posean
>  tickets aprobados con código mayor a 1000 podría ser la siguiente:
> 
>     `SELECT nombre FROM Área 
>     WHERE id IN (SELECT id_area FROM Ticket 
>     WHERE estado = 'aprobado' AND id > 1000);`

## 4. ¿Cuál es la forma correcta de crear una nueva migración en Laravel?
La forma correcta de crear una nueva migración en Laravel es mediante el uso del comando "php artisan make:migration" en la línea de comandos. Este comando toma un nombre de argumento que especifica el nombre de la migración y opcionalmente una opción de --create o --table que especifica el nombre de la tabla a crear o modificar.

Por ejemplo, si quieres crear una migración para crear una tabla llamada "users", el comando sería:

`php artisan make:migration create_users_table --create=users` 

O si deseas crear una migración para modificar una tabla existente llamada "users" el comando sería:

`php artisan make:migration modify_users_table --table=users` 

Una vez que hayas creado una migración, puedes ejecutarla usando el comando "php artisan migrate" para aplicar las modificaciones en la base de datos, y "php artisan migrate:rollback" para deshacer las últimas migraciones aplicadas.

## 5. ¿Cómo puedo crear un nuevo controlador en Laravel?

Puedes crear un nuevo controlador en Laravel mediante el uso del comando "php artisan make:controller" en la línea de comandos. Este comando toma un nombre de argumento que especifica el nombre del controlador y opcionalmente una opción --resource que indica que se debe crear un controlador de recursos.

Por ejemplo, si quieres crear un controlador llamado "UserController" el comando sería:

`php artisan make:controller UserController` 

Si deseas crear un controlador de recurso llamado "UserController" el comando sería:

`php artisan make:controller UserController --resource` 

Una vez que hayas creado el controlador, puedes agregar métodos para manejar las acciones de tu aplicación, como por ejemplo una función "index" para manejar la acción de ver una lista de usuarios, o una función "store" para manejar la acción de crear un nuevo usuario.

Es recomendable que también agregues las rutas correspondientes en el archivo web.php o api.php para poder acceder a las acciones del controlador desde la url.

## 6. ¿Cuál es la diferencia entre una ruta de tipo GET y una ruta de tipo POST en Laravel?

En Laravel, las rutas de tipo GET y POST son dos tipos diferentes de rutas que se utilizan para manejar peticiones HTTP diferentes.

Una ruta de tipo GET se utiliza para recuperar información del servidor. Por ejemplo, una ruta de tipo GET podría ser utilizada para cargar una página de inicio o para recuperar una lista de elementos de una base de datos. Por defecto, todas las peticiones que haga el navegador a través de un enlace o escribiendo la url en el navegador son de tipo GET.

Por otro lado, una ruta de tipo POST se utiliza para enviar información al servidor. Por ejemplo, una ruta de tipo POST podría ser utilizada para enviar un formulario de registro de un usuario o para crear un nuevo elemento en una base de datos. Las peticiones de tipo POST son enviadas al servidor a través de un formulario HTML.

En resumen, una ruta de tipo GET se utiliza para recuperar información, mientras que una ruta de tipo POST se utiliza para enviar información al servidor. Es importante asegurarse de utilizar el método correcto en las rutas correspondientes para evitar problemas de seguridad y garantizar un correcto funcionamiento de la aplicación.

## 7. ¿Cómo puedo validar una solicitud en Laravel? ¿Puedes proporcionar un ejemplo?

En Laravel, puedes validar una solicitud utilizando el componente de validación incluido en el framework. El proceso de validación se puede realizar dentro de un controlador o una clase de servicio.

Un ejemplo de cómo validar una solicitud en un controlador podría ser el siguiente:

    use Illuminate\Http\Request;
    use Illuminate\Validation\Rule;
    
    class UserController extends Controller
    {
        public function store(Request $request)
        {
            $validatedData = $request->validate([
                'name' => ['required', 'string', 'max:255'],
                'email' => ['required', 'string', 'email', 'max:255', Rule::unique('users')->ignore($user->id)],
                'password' => ['required', 'string', 'min:8'],
            ]);
    
            // Se puede proceder a crear un nuevo usuario con los datos validados
            User::create($validatedData);
        }
    }

En este ejemplo, estamos usando el método validate() del objeto Request para validar los datos de la solicitud. Estamos especificando las reglas de validación para cada campo en un arreglo asociativo. El nombre del campo es la clave del arreglo y las reglas de validación son los valores. La función create() de Eloquent ORM se encarga de crear un nuevo usuario con los datos validados.

El framework cuenta con muchas reglas de validación predefinidas como 'required', 'string', 'email', 'unique', 'min', 'max' entre otras, y también te permite crear tus propias reglas de validación personalizadas.

Es importante también mencionar que puedes personalizar los mensajes de error en caso de no cumplir las reglas establecidas, para ello debes crear un archivo en la carpeta resources/lang/es (o el idioma que uses) con el nombre validation.php y agregar los mensajes correspondientes.

## 8. ¿Cómo puedo hacer una consulta en una base de datos en Laravel? ¿Puedes proporcionar un ejemplo de una consulta de selección?
