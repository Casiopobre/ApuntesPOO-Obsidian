##### 1. ¿Cuál o cuáles de las siguientes características son únicas de la programación orientada a objetos? (1.00 puntos)
- [ ] Encapsulación
- [ ] Mantenimiento
- [ ] Polimorfismo
- [ ] Reutilización
- [ ] Modularidad
- [ ] Herencia
###### Respostas:
- [x] Encapsulación
- [ ] Mantenimiento
- [x] Polimorfismo
- [ ] Reutilización
- [ ] Modularidad
- [x] Herencia

##### 2. ¿Cuáles de las siguientes sentencias sobre los atributos primitivos son CIERTAS? (1.00 puntos)
- [ ] Se almacenan en la parte de la memoria conocida como montón.
- [ ] Ocupan menos memoria que los objetos.
- [ ] En el paradigma de POO tiene sentido hablar de ellos.
- [ ] No se puede hacer aliasing sin ellos.
- [ ] Es necesario reservar memoria explícitamente para ellos.
###### Respostas:
- [ ] Se almacenan en la parte de la memoria conocida como montón.
- [ ] Ocupan menos memoria que los objetos.
- [ ] En el paradigma de POO tiene sentido hablar de ellos.
- [ ] No se puede hacer aliasing sin ellos.
- [ ] Es necesario reservar memoria explícitamente para ellos.

##### 3. En Java, los atributos de una clase: (1.00 puntos)
- [ ] Deberían de ser siempre privados (private).
- [ ] Únicamente se reserva memoria para ellos en la pila y en el montón.
- [ ] Pueden ser accedidos por todos los métodos de la clase, independientemente de si esos métodos son privados.
- [ ] Deben inicializarse en el momento en que se declaran.
- [ ] No tiene sentido que un atributo sea `final` y `static`.
- [ ] Los únicos métodos que pueden modificar los valores de los atributos son los setters.
- [ ] En ningún caso tiene sentido que sean públicos (public).
###### Respostas:
- [x] Deberían de ser siempre privados (private).
- [x] Únicamente se reserva memoria para ellos en la pila y en el montón.
- [x] Pueden ser accedidos por todos los métodos de la clase, independientemente de si esos métodos son privados.
- [ ] Deben inicializarse en el momento en que se declaran.
- [ ] No tiene sentido que un atributo sea `final` y `static`.
- [ ] Los únicos métodos que pueden modificar los valores de los atributos son los setters.
- [ ] En ningún caso tiene sentido que sean públicos (public).

##### 4. ¿Cuáles de las siguientes afirmaciones sobre modificadores de acceso a atributos y métodos son FALSAS? (1.00 puntos)
- [ ] Si un atributo tiene acceso a paquete, podrá ser accedido directamente por los métodos de cualquier clase.
- [ ] Los métodos no pueden tener un modificador de acceso a paquete.
- [ ] La única forma de acceder a los atributos públicos de una clase es a través de los métodos de dicha clase.
- [ ] Un método privado de una ClaseA no puede acceder directamente a los atributos públicos de una ClaseB.
- [ ] Un método público de una ClaseA no puede acceder directamente a los atributos privados de una ClaseB.
- [ ] No tiene sentido que los métodos de una clase sean privados (private).
###### Respostas:
- [x] Si un atributo tiene acceso a paquete, podrá ser accedido directamente por los métodos de cualquier clase.
- [x] Los métodos no pueden tener un modificador de acceso a paquete.
- [x] La única forma de acceder a los atributos públicos de una clase es a través de los métodos de dicha clase.
- [x] Un método privado de una ClaseA no puede acceder directamente a los atributos públicos de una ClaseB.
- [ ] Un método público de una ClaseA no puede acceder directamente a los atributos privados de una ClaseB.
- [x] No tiene sentido que los métodos de una clase sean privados (private).

##### 5. ¿Cuáles de las siguientes sentencias sobre arrays (Tipo[]), ArrayList y HashMap son CIERTAS O CORRECTAS? (1.00 puntos)
- [ ] No es necesario reservar memoria para un array de int.
- [ ] Los elementos de un ArrayList pueden ser arrays.
- [ ] Si necesitamos recorrer todos los elementos de un conjunto de datos, es preferible usar un array que un HashMap.
- [ ] El acceso a un elemento de un array y de un ArrayList se realiza a través de un índice.
- [ ] Es posible acceder directamente a todos los elementos de un HashMap.
- [ ] En general, para almacenar un conjunto de objetos, es siempre preferible usar un ArrayList en vez de un array.
###### Respostas:
- [ ] No es necesario reservar memoria para un array de int.
- [x] Los elementos de un ArrayList pueden ser arrays.
- [x] Si necesitamos recorrer todos los elementos de un conjunto de datos, es preferible usar un array que un HashMap.
- [x] El acceso a un elemento de un array y de un ArrayList se realiza a través de un índice.
- [ ] Es posible acceder directamente a todos los elementos de un HashMap.
- [ ] En general, para almacenar un conjunto de objetos, es siempre preferible usar un ArrayList en vez de un array.

##### 6. ¿Cuáles de las siguientes afirmaciones sobre constructores son CIERTAS o CORRECTAS? (1.00 puntos)
Dada una clase llamada Libro con un atributo de tipo Libro llamado lib y un atributo
de tipo entero llamado num;
```java
    public Libro(int num) {
        this.num = num;
        lib = new Libro();
    }
```
- [ ] Los constructores se invocan para reservar memoria para cualquier tipo de dato.
- [ ] Los constructores son los únicos lugares de las clases en los que se deberían inicializar los atributos.
- [ ] Si un método lanza una excepción, necesariamente debe incluir la llamada a `throw` en alguna parte de su código.
- [ ] Un método puede capturar más de una excepción a través de varias cláusulas `catch`.
###### Respostas:
- [ ] Los constructores se invocan para reservar memoria para cualquier tipo de dato.
- [ ] Los constructores son los únicos lugares de las clases en los que se deberían inicializar los atributos.
- [ ] Si un método lanza una excepción, necesariamente debe incluir la llamada a `throw` en alguna parte de su código.
- [x] Un método puede capturar más de una excepción a través de varias cláusulas `catch`.

##### 7. ¿Cuáles de las siguientes afirmaciones relativas a polimorfismo son CIERTAS? (1.00 puntos)
- [ ] El polimorfismo en herencia se entiende como el uso del puntero `super`.
- [ ] En `ArrayList<Libreria>` se pueden almacenar instancias de cualquier clase que sea subclase de la clase `Libreria`.
- [ ] En el polimorfismo, una instancia de una clase únicamente se puede comportar como una instancia de dicha clase o de la clase padre de la clase.
- [ ] Si `ClaseA` es una subclase de `ClaseB` y `ClaseB` es una subclase de `ClaseC`, entonces la siguiente sentencia no es correcta: `ClaseA a = (ClaseA) new ClaseC();`.
- [ ] El operador `instanceof` se utiliza para averiguar si la clase de la cual es instancia un objeto.
- [ ] El polimorfismo de objetos está directamente relacionado con la sobrecarga de métodos.
###### Respostas:
- [ ] El polimorfismo en herencia se entiende como el uso del puntero `super`.
- [x] En `ArrayList<Libreria>` se pueden almacenar instancias de cualquier clase que sea subclase de la clase `Libreria`.
- [ ] En el polimorfismo, una instancia de una clase únicamente se puede comportar como una instancia de dicha clase o de la clase padre de la clase.
- [x] Si `ClaseA` es una subclase de `ClaseB` y `ClaseB` es una subclase de `ClaseC`, entonces la siguiente sentencia no es correcta: `ClaseA a = (ClaseA) new ClaseC();`.
- [ ] El operador `instanceof` se utiliza para averiguar si la clase de la cual es instancia un objeto.
- [ ] El polimorfismo de objetos está directamente relacionado con la sobrecarga de métodos.

##### 8. ¿Cuáles de las siguientes afirmaciones relativas a interfaces son FALSAS? (1.00 puntos)
- [ ] El cuerpo de los métodos de un interface debe estar vacío.
- [ ] Cada clase del programa debería tener asociado un interface en el que se declaran los métodos más importantes.
- [ ] Los interfaces se utilizan para independizar la implementación de clases.
- [ ] Los atributos de un interface pueden ser de acceso a paquete.
- [ ] Una clase no puede implementar dos interfaces que tengan dos métodos que se declaran de la misma forma (se llaman lo mismo, tienen los mismos argumentos y devuelven lo mismo).
- [ ] Los métodos declarados en un interface pueden ser abstractos (`abstract`).
###### Respostas:
- [ ] El cuerpo de los métodos de un interface debe estar vacío.
- [x] Cada clase del programa debería tener asociado un interface en el que se declaran los métodos más importantes.
- [x] Los interfaces se utilizan para independizar la implementación de clases.
- [ ] Los atributos de un interface pueden ser de acceso a paquete.
- [x] Una clase no puede implementar dos interfaces que tengan dos métodos que se declaran de la misma forma (se llaman lo mismo, tienen los mismos argumentos y devuelven lo mismo).
- [ ] Los métodos declarados en un interface pueden ser abstractos (`abstract`).

##### 9. Indicar y corregir los errores del siguiente código asumiendo que, (2.0 puntos)
- El interface y las clases se encuentran en archivos diferentes que tienen sus respectivos nombres.
- Las dos clases se encuentran en paquetes diferentes.
- La función `calcularPresupuesto( )` obtiene el presupuesto de una empresa para todo el año.
- Existen diferentes tipos de empleados (por ejemplo, Directivo, Administrativo, Gerente, etc.).
- No hay que introducir ninguna línea de código adicional, pero es posible que haya que borrar alguna línea de código.
```java
1  public interface IEmpresa {
2      public int getEmpleados( );
3      public boolean darAltaEmpleado(String empleado);
4      public boolean darBajaEmpleado(int pos) { };
5      private int calcularPresupuesto( );
6  }
7  
8  public final class Empresa implements IEmpresa {
9      ArrayList<Empleado> empleados;
10     public ArrayList< > getEmpleados( ) { return empleados; }
11     public boolean darBajaEmpleado(int pos) { empleados.remove(pos); }
12     public float calcularPresupuesto( );
13 }
14 
15 public class Informatica extends Empresa {
16     public float calcularPresupuesto( ) {
17         float presupuesto = calcularPresupuesto( );
18         for(int i = 0; i < empleados.size(); i++) {
19             if(empleados.get(i).equals(Directivo)) presupuesto = presupuesto + 3500;
20             else presupuesto = presupuesto + 900;
21         }
22         return presupuesto;
23     }
24     public boolean darAltaEmpleado (Empleado empleado);
25 }
```
