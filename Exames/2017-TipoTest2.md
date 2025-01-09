##### 1. ¿Cuál o cuáles de las siguientes afirmaciones relativas a [[Tema 4. Herdanza#Clases abstractas|clases abstractas]] son FALSAS? (1.00 puntos)
- [ ] Las clases abstractas no se pueden instanciar.
- [ ] Todos los métodos de las clases abstractas deben ser métodos abstractos.
- [ ] Las clases abstractas no pueden ser subclases de clases no abstractas.
- [ ] Las clases abstractas no deberían ocupar el último nivel de una jerarquía de clases.
- [ ] El objetivo de las clases abstractas es favorecer la reutilización.
- [ ] Las clases abstractas pueden tener métodos finales.
- [ ] En las clases abstractas no puede realizarse [[Tema 5. Polimorfismo#Poliformismo en herdanza|polimorfismo]] de métodos.
- [ ] Las únicas clases que pueden tener métodos abstractos son las clases abstractas.
###### Respostas:
- [ ] Las clases abstractas no se pueden instanciar.
- [x] Todos los métodos de las clases abstractas deben ser métodos abstractos.
- [x] Las clases abstractas no pueden ser subclases de clases no abstractas.
- [ ] Las clases abstractas no deberían ocupar el último nivel de una jerarquía de clases.
- [ ] El objetivo de las clases abstractas es favorecer la reutilización.
- [ ] Las clases abstractas pueden tener métodos finales.
- [x] En las clases abstractas no puede realizarse polimorfismo de métodos.
- [ ] Las únicas clases que pueden tener métodos abstractos son las clases abstractas.
##### 2. ¿Cuál o cuáles de las siguientes afirmaciones relativas a las interfaces y a la herencia son FALSAS? (1.00 puntos)
- [ ] Los interfaces no se pueden heredar por ninguna clase.
- [ ] Una clase abstracta no puede implementar ningún interface.
- [ ] Un interface no puede ser heredado por ningún interface.
- [ ] Cualquier clase de una jerarquía de clases puede invocar los métodos de un interface.
- [ ] El uso de los interface habilita la construcción de jerarquías con herencia múltiple.
- [ ] Un interface no puede heredar los métodos de una clase salvo que esa clase sea abstracta.
- [ ] Cualquier clase de una jerarquía de clases puede implementar un interfaz.
###### Respostas:
- [x] Los interfaces no se pueden heredar por ninguna clase.
- [x] Una clase abstracta no puede implementar ningún interface.
- [x] Un interface no puede ser heredado por ningún interface.
- [x] Cualquier clase de una jerarquía de clases puede invocar los métodos de un interface.
- [ ] El uso de los interface habilita la construcción de jerarquías con herencia múltiple.
- [x] Un interface no puede heredar los métodos de una clase salvo que esa clase sea abstracta.
- [ ] Cualquier clase de una jerarquía de clases puede implementar un interfaz.
##### 3. ¿Cuál o cuáles de las siguientes afirmaciones relativas a [[Tema 4. Herdanza#Clases, atributos e métodos finais|jerarquías de clases]] son FALSAS? (1.00 puntos)
- [ ] Las clases finales no pueden tener subclases.
- [ ] Las clases que no son ni finales ni abstractas no contribuyen a la reutilización de código.
- [ ] Las clases finales pueden ser clases abstractas.
- [ ] En una jerarquía debería haber siempre una única clase abstracta que se sitúa en el primer nivel (en la raíz) de la jerarquía.
- [ ] Las clases que no son finales pueden tener métodos finales.
- [ ] Una clase final podría ocupar el primer nivel de la jerarquía de clases.
###### Respostas:
- [ ] Las clases finales no pueden tener subclases.
- [x] Las clases que no son ni finales ni abstractas no contribuyen a la reutilización de código.
- [x] Las clases finales pueden ser clases abstractas.
- [ ] En una jerarquía debería haber siempre una única clase abstracta que se sitúa en el primer nivel (en la raíz) de la jerarquía.
- [ ] Las clases que no son finales pueden tener métodos finales.
- [ ] Una clase final podría ocupar el primer nivel de la jerarquía de clases.

##### 4. ¿Cuáles de las siguientes afirmaciones sobre herencia en Java son CIERTAS? (1.00 puntos)
- [ ] Las clases padre deberían tener más atributos que las clases hijas.
- [ ] Las clases hijas son una extensión de las clases padre.
- [ ] Los constructores se heredan para favorecer la reutilización de código.
- [ ] Los modificadores de los atributos deben ser `private` para prevenir la copia indiscriminada de atributos en las clases.
- [ ] Si la `ClaseA` es una subclase de la `ClaseB`, entonces en la clase `ClaseA` la palabra reservada `super` se podrá usar para llamar únicamente a los métodos de la `ClaseB` que son protegidos (`protected`) y públicos (`public`).
- [ ] El puntero `super` favorece la reutilización de código entre las clases de la jerarquía.
###### Respostas:
- [ ] Las clases padre deberían tener más atributos que las clases hijas.
- [v] Las clases hijas son una extensión de las clases padre.
- [ ] Los constructores se heredan para favorecer la reutilización de código.
- [ ] Los modificadores de los atributos deben ser `private` para prevenir la copia indiscriminada de atributos en las clases.
- [v] Si la `ClaseA` es una subclase de la `ClaseB`, entonces en la clase `ClaseA` la palabra reservada `super` se podrá usar para llamar únicamente a los métodos de la `ClaseB` que son protegidos (`protected`) y públicos (`public`).
- [v] El puntero `super` favorece la reutilización de código entre las clases de la jerarquía.


##### 5. Teniendo en cuenta el siguiente extracto de código, ¿cuál o cuáles de las siguientes afirmaciones son CIERTAS? (1.00 puntos)
```java
public class Mensajeria {
    public static float MAXIMO_CLIENTES_LIBRERIA = 500;
    private double paquetesNoRecibidos;
    protected Vector paquetesEnviadosPorDia;
    Hashtable<Vector<Paquete>, Fecha> paquetesEnviados;
    ...
}
```
- [ ] El atributo `paquetesNoRecibidos` no podrá ser heredado por ninguna clase hija de la clase `Mensajeria`.
- [ ] El atributo `paquetesEnviados` puede ser heredado por cualquier clase.
- [ ] El atributo `paquetesNoRecibidos` no puede ser utilizado por los métodos de una clase hija de `Mensajeria`.
- [ ] El atributo `paquetesEnviadosPorDia` puede ser heredado por cualquier clase hija de la clase `Mensajeria`.
- [ ] El atributo `MAXIMO_CLIENTES_LIBRERIA` no puede ser heredado por ninguna clase hija de la clase `Mensajeria` como una constante.
###### Respostas:
- [v] El atributo `paquetesNoRecibidos` no podrá ser heredado por ninguna clase hija de la clase `Mensajeria`.
- [v] El atributo `paquetesEnviados` puede ser heredado por cualquier clase.
- [v] El atributo `paquetesNoRecibidos` no puede ser utilizado por los métodos de una clase hija de `Mensajeria`.
- [v] El atributo `paquetesEnviadosPorDia` puede ser heredado por cualquier clase hija de la clase `Mensajeria`.
- [ ] El atributo `MAXIMO_CLIENTES_LIBRERIA` no puede ser heredado por ninguna clase hija de la clase `Mensajeria` como una constante.

##### 6. Indicar y corregir los errores en el siguiente código (1.00 puntos)
+ El interface y las clases se encuentran en archivos distintos con sus nombres correctos y las dos clases se encuentran en paquetes distintos.
+ La clase Libro es la clase raíz de una jerarquía de clases sobre tipos de libros y tiene todos los setters y getters implementados.
+ Es posible que existan tiendas en las que solo se vendan revistas de diferente tipo (por ejemplo, revistas científicas, del corazón, económicas, etc.) Además, la clase TiendaRevistas no puede ser abstracta.
+ No hay que introducir ninguna línea de código adicional, pero es posible que haya que borrar alguna línea de código.

```java
public interface Librería {
    private static String DOMINIO = "Temas bibliográficos";
    public int getNumeroLibros();
    public String getISBNLibro(String idLibro);
    public ArrayList<Libro> obtenerLibros();
}

public abstract class LibreriaImpl extends Librería {
    ArrayList<Libro> listaLibros;
    public ArrayList<Libro> obtenerLibros() { return listaLibros; }
    public String getISBNLibro(Libro libro) { return libro.getISBN(); }
    public getNumeroLibros();
    public int numeroLibrosAccion();
}

public final class TiendaRevistas extends LibreriaImpl {
    public int numeroLibrosAccion() {
        super.numeroLibrosAccion();
        int num = 0;
        for (int i = 0; i < listaLibros.size(); i++) {
            if (listaLibros.get(i).equals("Accion")) num++;
        }
        return num;
    }
    public int getNumeroLibros();
}
```
###### A miña resposta:
```java
public interface Librería {
    public static final String DOMINIO = "Temas bibliográficos"; // <-
    public int getNumeroLibros();
    public String getISBNLibro(Libro libro);
    public ArrayList<Libro> obtenerLibros();
}

public abstract class LibreriaImpl implements Librería { // <---------
    protected ArrayList<Libro> listaLibros; // <-------------------
    public ArrayList<Libro> obtenerLibros() { return listaLibros; }
    public String getISBNLibro(Libro libro) {return libro.getISBN(); }
    public int getNumeroLibros() {return listaLibros.size()}; // <------
    public abstract int numeroLibrosAccion(); // <---------------------
}

public final class TiendaRevistas extends LibreriaImpl {
    public int numeroLibrosAccion() {
        super.numeroLibrosAccion();
        int num = 0;
        for (int i = 0; i < super.listaLibros.size(); i++) {
            if (listaLibros.get(i) instanceof Accion) num++; // <----
        }
        return num;
    }
    public int getNumeroLibros() {super.getNumeroLibros()}
}
```
###### Respostas:
```java
public interface Librería {
    public final static String DOMINIO = "Temas bibliográficos"; // <--
    public int getNumeroLibros();
    public String getISBNLibro(Libro idLibro); // <--------------------
    public ArrayList<Libro> obtenerLibros();
}

public abstract class LibreriaImpl implements Librería { //<-----------
    private ArrayList<Libro> listaLibros; // <-------------------------
    public ArrayList<Libro> obtenerLibros() { return listaLibros; }
    public String getISBNLibro(Libro libro) { return libro.getISBN(); }
    public int getNumeroLibros(){ return listaLibros.size();}; // <----
    public abstract int numeroLibrosAccion(); // <---------------------
}

public class TiendaRevistas extends LibreriaImpl { // <----------------
    public int numeroLibrosAccion() {
        super.numeroLibrosAccion();
        int num = 0;
        for (int i = 0; i < listaLibros.size(); i++) {
            if (listaLibros.get(i) instanceof Accion) num++; // <-----
        }
        return num;
    }
    public int getNumeroLibros();
}
```