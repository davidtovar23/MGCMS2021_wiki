# Usuarios

En esta sección se abordarán el Módulo de Usuarios con sus respectivos
submódulos: Usuarios y Perfiles.  
Para acceder a cada uno, haga clic en el
módulo Usuarios, este desplegara los submódulos y solo requerirá dar otro clic
en el submódulo al que desee ingresar.  

<img src="images/usuarios/pantallas/menu_usuarios.png" width="200px">
<br><br>

NOTA: Debe tener un rol como *super_admin*, o tener un perfil con los permisos
necesarios para poder crear usuarios, roles y permisos.

## Tabla de contenido

- [Usuarios](#usuarios)
  - [Tabla de contenido](#tabla-de-contenido)
  - [Usuarios](#usuarios-1)
    - [Glosario de clases](#glosario-de-clases)
      - [Diagrama de flujo - Ver usuarios](#diagrama-de-flujo---ver-usuarios)
    - [Agregar Usuario](#agregar-usuario)
      - [Diagrama de flujo - Agregrar usuario](#diagrama-de-flujo---agregrar-usuario)
    - [Modificar Usuario](#modificar-usuario)
      - [Diagrama de flujo - Modificación de usuario](#diagrama-de-flujo---modificación-de-usuario)
    - [Eliminación de  Usuario](#eliminación-de--usuario)
      - [Diagrama de flujo - Eliminación de usuario](#diagrama-de-flujo---eliminación-de-usuario)
  - [Roles de usuario](#roles-de-usuario)
      - [Diagrama de flujo - Ver roles](#diagrama-de-flujo---ver-roles)
    - [Agregar rol](#agregar-rol)
      - [Diagrama de flujo - Agregrar rol](#diagrama-de-flujo---agregrar-rol)
    - [Modificar rol](#modificar-rol)
      - [Diagrama de flujo - Modificación de rol](#diagrama-de-flujo---modificación-de-rol)
    - [Eliminación de  rol](#eliminación-de--rol)
      - [Diagrama de flujo - Eliminación de rol](#diagrama-de-flujo---eliminación-de-rol)
  - [Permisos de usuario](#permisos-de-usuario)
      - [Diagrama de flujo - Ver permisos](#diagrama-de-flujo---ver-permisos)
    - [Agregar permiso](#agregar-permiso)
      - [Diagrama de flujo - Agregrar permiso](#diagrama-de-flujo---agregrar-permiso)
    - [Modificar permiso](#modificar-permiso)
      - [Diagrama de flujo - Modificación de permiso](#diagrama-de-flujo---modificación-de-permiso)
    - [Eliminación de  permiso](#eliminación-de--permiso)
      - [Diagrama de flujo - Eliminación de permiso](#diagrama-de-flujo---eliminación-de-permiso)

## Usuarios
Aparecerá en pantalla el listado de todos los usuarios registrados con acceso al CMS, la información relevante de cada uno y las opciones agregar, modificar, ver actividad
y eliminar, las cuales detallaremos a continuación. 

![Listado de usuarios](images/usuarios/pantallas/listado_usuarios.png)

### Glosario de clases
glosario de clases

#### Diagrama de flujo - Ver usuarios
![Ver usuarios](images/usuarios/diagramas/consulta_usuario.png)

### Agregar Usuario
Desde la sección de Usuarios de clic en el botón **Agregar Usuario**, lo llevara a la sección **Crear Usuario.**  

Aparecerá el siguiente formulario con diversos campos importantes para el
registro de nuevos usuarios

![Pantalla crear usuario](images/usuarios/pantallas/crear_usuario.png)

El campo "*Email address*", es el email con el que se ingresara al CMS junto con el campo contraseña.  

Es necesario seleccionar un **Rol** adecuado para el usuario, esto limitara las acciones que puede realizar dentro el CMS.  

Si no se encuentra el **Rol** indicado, pueds crearlo, para esto, revise la sub sección [Roles](#roles).  
En el apartado "*Sites*" se puede seleccionar los sitios a los que este usuario tendrá acceso.

Al finalizar el llenado de los campos es necesario dar clic en **Submit**, de lo contrario los cambios no se verán reflejados

#### Diagrama de flujo - Agregrar usuario
![Diagrama Crear usuario](images/usuarios/diagramas/agregar_usuario.png)


### Modificar Usuario
Desde la sección de Usuarios de clic en **Editar Usuario** del usuario que desea modificar y lo llevara a la sección **Modificar Usuario.**  

Aparecerá el siguiente formulario con la información del usuario.

![Pantalla Modificación usuario](images/usuarios/pantallas/modificacion_usuario.png)

Al finalizar el llenado de los campos es necesario dar clic en **Submit**, de lo contrario los cambios no se verán reflejados

#### Diagrama de flujo - Modificación de usuario
![Diagrama Crear usuario](images/usuarios/diagramas/modificacion_usuario.png)

### Eliminación de  Usuario
Desde la sección de Usuarios de clic en el botón **Eliminar** del usuario que desea eliminar y le mostrará un mensaje de confirmación

Aparecerá el siguiente mensaje de confirmación:

![Pantalla Modificación usuario](images/usuarios/pantallas/eliminacion_usuario.png)

Puede cancelar la acción si no esta seguro de eliminar el registro, al dar click en el botón **Ok** el usuario se eliminará y no se podrá recuperar el registro.

#### Diagrama de flujo - Eliminación de usuario
![Diagrama Eliminar usuario](images/usuarios/diagramas/eliminacion_usuario.png)




## Roles de usuario
Aparecerá en pantalla el listado de todos los roles registrados, la información de cada uno y las opciones agregar, modificar, asignar permisos y eliminar, las cuales detallaremos a continuación. 

![Pantalla Listado de roles](images/roles/pantallas/listado_roles.png)

#### Diagrama de flujo - Ver roles
![Ver roles](images/roles/diagramas/consulta_roles.png)

### Agregar rol
Desde la sección de roles de clic en el botón **Agregar rol**, lo llevara a la sección **Crear rol.**  

Aparecerá el siguiente formulario con diversos campos importantes para el
registro de nuevos roles

![Pantalla crear rol](images/roles/pantallas/agregar_rol.png)

Al finalizar el llenado de los campos es necesario dar clic en **Crear**, de lo contrario los cambios no se verán reflejados

#### Diagrama de flujo - Agregrar rol
![Diagrama Crear rol](images/roles/diagramas/agregar_rol.png)


### Modificar rol
Desde la sección de roles de clic en **Editar rol** del rol que desea modificar y lo llevara a la sección **Editar rol.**  

Aparecerá el siguiente formulario con la información del rol.

![Pantalla Modificación rol](images/roles/pantallas/modificacion_rol.png)

Al finalizar el llenado de los campos es necesario dar clic en **Actualizar**, de lo contrario los cambios no se verán reflejados

#### Diagrama de flujo - Modificación de rol
![Diagrama Crear rol](images/roles/diagramas/modificacion_rol.png)

### Eliminación de  rol
Desde la sección de roles de clic en el botón **Eliminar** del rol que desea eliminar y le mostrará un mensaje de confirmación

Aparecerá el siguiente mensaje de confirmación:

![Pantalla Modificación rol](images/roles/pantallas/eliminacion_rol.png)

Puede cancelar la acción si no esta seguro de eliminar el registro, al dar click en el botón **Ok** el rol se eliminará y no se podrá recuperar el registro.

#### Diagrama de flujo - Eliminación de rol
![Diagrama Eliminar rol](images/roles/diagramas/eliminacion_rol.png)


## Permisos de usuario
Aparecerá en pantalla el listado de todos los permisos registrados, la información de cada uno y las opciones agregar, modificar y eliminar, las cuales detallaremos a continuación. 

![Pantalla Listado de permisos](images/permisos/pantallas/listado_permisos.png)

#### Diagrama de flujo - Ver permisos
![Ver permisos](images/permisos/diagramas/consulta_permisos.png)

### Agregar permiso
Desde la sección de permisos de clic en el botón **Agregar permiso**, lo llevara a la sección **Crear permiso.**  

Aparecerá el siguiente formulario con diversos campos importantes para el
registro de nuevos permisos

![Pantalla crear permiso](images/permisos/pantallas/agregar_permiso.png)

Al finalizar el llenado de los campos es necesario dar clic en **Crear**, de lo contrario los cambios no se verán reflejados

#### Diagrama de flujo - Agregrar permiso
![Diagrama Crear permiso](images/permisos/diagramas/agregar_permiso.png)


### Modificar permiso
Desde la sección de permisos de clic en **Editar permiso** del permiso que desea modificar y lo llevara a la sección **Editar permiso.**  

Aparecerá el siguiente formulario con la información del permiso.

![Pantalla Modificación permiso](images/permisos/pantallas/modificacion_permiso.png)

Al finalizar el llenado de los campos es necesario dar clic en **Actualizar**, de lo contrario los cambios no se verán reflejados

#### Diagrama de flujo - Modificación de permiso
![Diagrama Crear permiso](images/permisos/diagramas/modificacion_permiso.png)

### Eliminación de  permiso
Desde la sección de permisos de clic en el botón **Eliminar** del permiso que desea eliminar y le mostrará un mensaje de confirmación

Aparecerá el siguiente mensaje de confirmación:

![Pantalla Eliminación permiso](images/permisos/pantallas/eliminacion_permiso.png)

Puede cancelar la acción si no esta seguro de eliminar el registro, al dar click en el botón **Ok** el permiso se eliminará y no se podrá recuperar el registro.

#### Diagrama de flujo - Eliminación de permiso
![Diagrama Eliminar permiso](images/permisos/diagramas/eliminacion_permiso.png)

[]