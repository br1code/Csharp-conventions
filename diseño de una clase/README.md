# Diseño de una clase

Una clase puede contener campos, propiedades, métodos, eventos, delegados, atributos y otros tipos. Ese será el alcance con el que trabajaremos, y para el final de este documento estará escribiendo clases de alta calidad que son fáciles de leer y mantener, incluso para otros desarrolladores que no han leído o trabajado con su código anteriormente.

Organizar su clase en una estructura mantenible es equivalente a mantener su armario organizado. Si guardo todas mis camisas, pantalones y medias en una solo cajón, no puedo encontrar todo lo que necesito sin la posibilidad de tener que pasar por todo lo demás. Puedo tener suerte y encontrar un par de pantalones en la parte superior del cajón, o tal vez no sea tan afortunado y tenga que tirar todo el contenido del cajón al piso.

Lo opuesto ocurre cuando mantengo mi armario organizado. Si tengo mis pantalones y medias doblados y los coloco en sus propios compartimientos, y mis camisas están en perchas, puedo encontrar fácilmente todo lo que necesito sin tener que desorganizar nada.

Lo mismo vale para tu estructura de clase. **Si escribe cada clase con la misma estructura, cada clase se vuelve muy fácil de leer y mantener**.

La estructura de su clase se define por el orden y la agrupación de la API pública y los detalles de implementación.

Los campos deben definirse en un lugar y los métodos en otro. Lo mismo ocurre con las propiedades, eventos, delegados y tipos anidados (clases dentro de clases).

Al estructurar su código de esta manera, su código sirve como una especie de índice que se puede leer y navegar fácilmente. **Para un diseño de clase óptimo y facil de mantener, use la siguiente estructura:**

> Escribiremos el código en inglés ya que es lo habitual en casi cualquier equipo de trabajo
```C#
// Copyright information

namespace CompanyName.Technology.Feature
{
    // Using directives
    // Global Delegates

    class ClassName
    {
        // 1. Fields, Constants
        // 2. Constructors
        // 3. Events
        // 4. Properties
        // 5. Methods
        // 6. Nested Types
    }
}
```

**DO** : Usa esta estructura de clases consistentemente en todas las clases que escribas.

**DO** : Reserve la primera parte del archivo para cualquier comentario de derechos de autor o avisos informativos importantes sobre el archivo de código fuente actual.

**DO** : Declare el uso de directivas en orden alfabético. Con Visual Studio tienes un comando para esto.

**DO** : Declare campos, campos de solo lectura, campos estáticos o constantes al comienzo de la definición de clase por grupo, y en orden alfabético.

**DO** : Declare constructores por orden de complejidad (número de parámetros), comenzando por el menos complejo hasta el más complejo.

**DO** : Declare eventos en orden alfabético.

**DO** : Declare propiedades en orden alfabético.

**DO** : Declare métodos en orden alfabético. Al declarar métodos polimórficos, debe declararlos por orden de complejidad (número de parámetros), comenzando por el menos complejo hasta el más complejo.

**DO** : Declare tipos anidados en orden alfabético.

**DO** : Declare solo un tipo por archivo y asigne un nombre al archivo después del tipo. Al declarar el tipo ClassName, cambie el nombre del archivo a ClassName.cs.

**DO NOT** : Dejar el nombre de un archivo como Class1.cs, Form1.cs, o cualquier nombre no identificable.

> No nombrar un archivo de código de forma apropiada dice algo acerca de su atención al detalle. Lleva muy poco tiempo nombrar un archivo que sea identificable y útil, y está ayudando a otros desarrolladores haciendo esto. Lo primero que haces al buscar en código fuente de un proyecto es ver los archivos, y tener que buscar entre docenas de archivos sin nombres significativos puede ser una pesadilla para otro desarrollador, especialmente para alguien nuevo o temporal al proyecto.

Ahora que establecimos una lista de lo que debe y no debe recordar, veamos un ejemplo de cómo una buena clase debería estar escrita.

```C#
namespace Br1Company.Project.Blog
{
    // Using directives
    using System;
    using System.Collections.Generic;

    public class Post
    {
        // 1. Fields
        private List<Comment> comments;
        private DateTime date;
        private string title;
        
        // Constructors
        public Post(string title)
        {
            this.comments = new List<Comment>();
            this.date = DateTime.Now;
            this.title = title;
        }

        // Events
        public event EventHandler<CommentEventArgs> CommentCreated;

        // Properties
        public string Date
        {
            get { return date; }
        }

        public string Title
        {
            get { return title; }
            set
            {
                if (!String.IsNullOrEmpty(value))
                {
                    title = value;
                }
            }
        }

        // Methods
        public void Comment(Comment comment)
        {
            comments.add(comment);
        }

        private void OnCommentCreated(Comment comment)
        {
            CommentCreated?.Invoke(this, new CommentEventArgs(comment));
        }
    }
}
```
Lo primero que debe destacarse es que la clase sigue la estructura descrita anteriormente. Comienza con el `namespace`, los `using`, la declaración `class`, luego algunos `fields`, un `constructor`, un `event`, algunas `properties` y finalmente unos `methods`.

Mantuve la clase lo suficientemente simple por ahora. Básicamente es una clase que representa un `Post`, el cual tiene algunos datos como el título y la fecha de creación, junto a una lista de `Comment`, la cual puede llenarse utilizando un método de esta clase. Además, incluye un evento que se invoca cuando un `Comment` es creado.

Siguiendo esta estructura, podemos ver que la clase se puede leer fácilmente como un índice. Encontrar lo que necesita es relativamente fácil de hacer, y esto se vuelve crítico cuando se trabaja con clases muy grandes.

La estructura y el diseño de una clase es un punto de partida fundamental para escribir clases de alta calidad, pero a pesar de que esta clase se ve muy simple, todavía está muy lejos de ser una clase de alta calidad. **Le faltan algunas características clave que la completan, lo que nos lleva a nuestra próxima sección**: 

## [Convenciones de Nombres](.//convenciones%20de%20nombres)

