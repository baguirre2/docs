Entidades
########

.. php:namespace:: Cake\ORM

.. php:class:: Entity

Mientras :doc:`/orm/table-objects` representa y provee acceso a la colección de objetos, las entidades representan filas individuales o dominio de objetos en su aplicación. Las entidades contienen propiedades persistentes y métodos para manipular y acceder a la información que contienen. 

Las entidades son creadas para usted por CakePHP cada vez que se usa ``find()`` en un objeto tabla. 

Creando Clases Entidad
=======================

Usted no necesita crear clases entidad para empezar a usar el ORM en CakePHP. 
Como sea, si desea tener una lógica personalizada en sus entidades necesitará crear clases. La conversión de clases en vivo en **src/Model/Entity/**. Si nuestra aplicación tiene la tabla ``articulos`` nosotros podremos crear la entidad siguiente:: 


    // src/Model/Entity/Articulo.php
    namespace App\Model\Entity;

    use Cake\ORM\Entity;

    class Articulo extends Entity
    {
    }

En este momento la entidad no hace mucho, cuando nosotros carguemos información de nuestra tabla artículos, obtendremos instancias de esta clase. 

.. note::

    Si no quiere definir una clase entidad, CakePHP usará una clase entidad básica.

Creando Entidades
=================

Las entidades pueden ser directamente instanciadas::

    use App\Model\Entity\Article;

    $articulo = new Articulo();

Cuando se instancia una entidad, se pueden pasar las propiedad con los datos que quiere almacenar en ellos::

    use App\Model\Entity\Articulo;

    $articulo = new Articulo([
        'id' => 1,
        'titulo' => 'Nuevo Articulo',
        'creacion' => new DateTime('now')
    ]);

Otra forma de obtener nuevas entidades es usando el método: ``newEntity()`` desde los objetos ``Table``::

    use Cake\ORM\TableRegistry;

    $articulo = TableRegistry::get('Articulos')->newEntity();
    $articulo = TableRegistry::get('Articulos')->newEntity([
        'id' => 1,
        'titulo' => 'Nuevo Articulo',
        'creacion' => new DateTime('now')
    ]);

Accediendo a los datos de la Entidad
=====================

Las entidades proveen algunas formas para acceder a los datos que contienen. Más comúnmente se puede acceder a los datos en una entidad usando la notación objeto::

    use App\Model\Entity\Article;

    $articulo = new Articulo;
    $articulo->titulo = 'Este es mi primer post';
    echo $articulo->titulo;

También es posible usar los métodos ``get()`` y ``set()``::

    $articulo->set('titulo', 'Este es mi primer post');
    echo $articulo->get('titulo');

Cuando se usa ``set()`` se pueden actualizar múltiples propiedades usando un arreglo::

    $articulo->set([
        'titulo' => 'Mi primer post',
        'cuerpo' => '¡Es el mejor de todos los tiempos!'
    ]);

.. warning::

        Cuando se actualizan las entidades con un ``request`` data, es esencial establecer cuales son los campos que se pueden actualizar en una asignación masiva.
        
