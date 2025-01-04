# Tema 2. Clases e tipos de datos: tipos primitivos, referencias e aliasing
## Tipos de datos primitivos
Son os tipos de datos **predefinidos** e teñen unha correspondencia directa cos tipos de datos de C.
Características:
+ _Tamaño fixo_
+ _Correspondencia directa_ cos tipos de datos representables por un ordenador
+ _Reserva de memoria automática_ ao declaralos
+ _Non teñen métodos_
+ _Non son clases_, xa que están directamente vinculados aos valores das variables

Para asegurar a consistencia do esquema de datos de Java, definíronse **wrappers**: _clases de Java que encapsulan o valor do tipo de dato_ e lle proporcionan _métodos_ útiles, que permiten obter o valor do dato, convertilo nunha string ou castealo a outros tipos de datos primitivos. 
![[Pasted image 20241224140652.png | center | 250]]

_Problema_: o emprego de wrappers xera un código moito máis _dificil de comprender_
_Solución_: empregar **autoboxing e unboxing**, que _permite tratar un wrapper coma se fose un tipo primitivo_ e viceversa.
+ **Autoboxing**: convirte un ==tipo primitivo a== un obxecto da súa clase ==wrapper== correspondente. Aplícase cando:
		a) Un método ten como arg un tipo wrapper e recibe un tipo primitivo
		b) A un tipo wrapper se lle asigna un valor de tipo primitivo
```java
public static void main(String[] args){
	Integer aa = 10; // Autoboxing
	Integer bb = 20; // Autoboxing
	if (aa > bb) // Java traduce a aa.intValue()>bb.intValue()
		System.out.println("aa + bb = " + suma(aa, bb)); 
}

public static int suma(int a, int b){ // Unboxing
	return a + b;
}
```

+ **Unboxing**: convirte un obxecto ==wrapper ao tipo primitivo== correspondente. Aplícase cando:
		a) Un método ten como arg un tipo primitivo e recibe un tipo wrapper
		b) A un tipo primitivo se lle asigna un obxeto tipo wrapper
```java
public static void main(String[] args){
	int aa = new Integer(10); // Unboxing
	int bb = new Integer(20); // Unboxing
	if (aa > bb) 
		System.out.println("aa + bb = " + suma(aa, bb)); 
}

public static int suma(Integer a, Integer b){ // Autoboxing
	return a + b;
}
```
Principal beneficio do unboxing: cando os métodos teñen como args os wrappers.
**==!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!==** **[[Preguntas tipo exame POO#Pregunta 1 Tema 2. Unboxing e Autoboxing| PREGUNTA DE EXAME!!!]]** **==!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!==**

## Referencias
### Aliasing
En Java, os **nomes dos obxetos son referencias** á posición de memoria reservada para eles. Esto implica que cando se lle asigna un obxeto A a outro obxeto B, _non se realiza unha copia_, senon que se lle asigna a referencia do obxeto B á referencia do obxeto A (polo que _ambos apuntan á mesma dirección de memoria_), así que a memoria de A xa non está dispoñible.
![[Pasted image 20241224164527.png | center]]

Esta asignación de referencias entre obxetos denomínase **==aliasing==**, é e unha das principales caracteristicas da programación orientada a obxetos. _Evita a encapsulación dos datos_, xa que permite modificar o valor dos atributos dunha clase dende métodos doutra clase.

> "The big lie of object-oriented programming is that objects provide encapsulation"

> [!Exemplo]
> Na liña 3 ocorre aliasing: agora `paises` apunta á mesma dirección de memoria que o conxunto de países designados ao xogador (atributo) (`jugador.getPaises()`). Polo tanto, despois, na liña 4, elimínase o primeiro obxeto de paises, e, debido ao aliasing, tamen da arraylist do atributo paises de xogador.
```java
1 public static void main(String[] args) {
2     Jugador jugador = new Jugador("Luis", Valor.EJERCITO_AZUL, mapa);
3     ArrayList<Pais> paises = jugador.getPaises();
4     paises.remove(0);
5 }
```

_Problema_ do aliasing: os programas son máis difíciles de manter, xa que os valores dos atributos se poden modificar en calquera parte do programa de forma descontrolada. Pero tampouco é viable evitar o aliasing xa que precisaríase dunha copia completa da zona de memoria referenciada.
_Solución_: seleccionar as partes do código nas que hai que evitar o aliasing, introducindo _manualmente_ código que xere unha nova referencia ao obxeto.
+ Un método, en vez de devolver unha referencia a un atributo, deberá _crear e devolver un obxeto_ do mesmo tipo do atributo, pero que ocupe unha dirección de memoria diferente (o mesmo cando un método acepte como entrada a referencia dun obxeto).
Para facilitar esto: método **clone**.
### Método clone
Este método **xera unha copia dun obxeto** e a almacena nunha **posición de memoria diferente**.
+ Débese implementar _explícitamente_ o método clone _para cada clase_ de cuxos obxetos se queira realizar unha copia.
+ Non é óptimo implementalo en todas as clases, especialmente se se trata de realizar _copias profundas_, onde hai que reservar memoria para todos os atributos da clase (incluíndo todos os elementos dun conxunto de datos).
>[!Exemplo]
> Na liña 7, é necesario _xerar un novo obxeto do tipo `Mapa`_, chamando a `clone`, que debería estar implementado na clase `Mapa`. Despois no bucle da liña 9 é necesario _reservar memoria para cada país_ e copiar todos os valores dos seus atributos cun `clone`.
```java
0 @Override
1 public Object clone(){
2 	try{
3 		super.clone();
4 	} catch(CloneNotSupportedException exc){
5 		System.out.println(exc.getMessage());
6 	}
7 	Jugador jugador = new Jugador(nombre, color, (Mapa) mapa.clone());_
8 	ArrayList<Pais> paisesClonados = new ArrayList<>();
9 	for(int i = 0; i < paises.size(); i++)
10 		paisesClonados.add((Pais) paises.get(i).clone());
11 	return jugador;
12 }
```

## Máquina virtual de Java
É a encargada da execución dun programa en Java. 
![[Pasted image 20241224194422.png | center]]

## Almacenamento
### Datos
Os datos almacénanse de forma distinta según o tipo de dato e o lugar do programa no que se definan:
+ **Pila**: zona da memoria á que o procesador ten _acceso directo_ a través do stack pointer, polo que a lectura e escritura é rápida e eficiente.
	+ As variables só existen na pila _durante a execución do método que as creou_.
	+ Os datos que se almacenan na pila deben ter sempre un *tamaño coñecido* :
		+ Todo o _código_ dos métodos (_call stack_)
		+ Todos os _datos_ de tipo _primitivos_
		+ As _referencias_ aos obxetos creados no programa 
+ **Montón**: zona da memoria na que o procesador non precisa de coñecer a cantidade de memoria que é necesario reservar para uns datos nin o tempo que deben estar dispoñibles os mesmos.
	+ _Almacena os obxetos_ creados durante a execución do programa
	+ Os datos non se eliminan de forma automática: _recolector de lixo_
	+ A sua xestion condiciona en gran medida o _rendemento_ de un programa en Java

> [!Exemplo]
> Onde se almacenan os datos deste programa?
> + **Na pila**:
> 	+ As _variables locales do main_: `enteroLocal`almacénase directamente na pila (tipo primitivo) e `cadenaLocal` almacénase como unnha referencia ao montón (xa que é unha String). Ademáis, tamen se almacena na pila a referencia ao obxeto/instancia `e` (que se atopa no montón, como a String).
> 	+ O _código das funcións da clase_ (os setters): as variables `x` e `s` apuntan aos mesmos valores que as variables do main por aliasing (debido a empregar os setters).
> + **No montón**:
> 	+ A _instancia_ da clase `EjemploStackYHeap` creada no main, cos seus atributos `Entero` e `Cadena`.
> 	+ A String "atributo" (como en C).

```java
public class EjemploStackYHeap { // Clase cun int e unha String
    private int Entero;
    private String Cadena;

    public void setEntero(int x) {
        atributoEntero = x;
    }

    public void setCadena(String s) {
        Cadena = s;
    }
}

public class Principal {
    public static void main(String[] a) {
        int enteroLocal = 5;
        String cadenaLocal = "atributo";

        EjemploStackYHeap e;  
        new EjemploStackYHeap(); // Creamos un obxeto/instancia 
        e.setEntero(enteroLocal); // Setteamos
        e.setCadena(cadenaLocal); //Setteamos
    }
}
```

![[Pasted image 20241225094806.png | center]]

### Métodos
Unha clase per se non ocupa memoria, senón que o código dos métodos se cargan na pila cando se _crea un obxeto_ desa clase (`Clase obxeto = new Clase();`). Cando xa se creou o obxeto, xa é posible acceder a todos os métodos a través do _operaor "."_, e cando no método se fai referencia a un atributo da clase á que pertence, este atributo toma os valores asociados ao obxeto que chama ao método. 

## Recolector de lixo
Encárgase de buscar na memoria do programa para **identificar e eliminar os obxetos que xa non se empregan** (_lixo_). Corre en _segundo plano_ á execución do programa e ten un _impacto directo no rendemento_ deste, xa que a eiminación do lixo fai máis doado acceder aos obxetos que sí se están a empregar no programa. Polo tanto, realiza unha _xestión máis eficiente_ da memoria, xa que evita erros derivados da xestión manual da memoria (como free en C).
### Proceso básico
1. **Marcado**: identifícanse que zonas de memoria están sendo usadas e cales non (pode resultar moi ineficiente)
	![[Pasted image 20241225114803.png | center | 400]]
2. **Borrado**: 
	+ Opción 1. _Borrado normal_: elimínanse de memoria os obxetos que non teñen referencias asignadas durante máis tempo e se mantén unha lista de posibles referencias á parte de memoria que pode ser empregada.
	![[Pasted image 20241225115318.png | center | 400]]
	 + Opción 2. _Borrado con compactación_: despois de borarr os obxetos non referenciados, se compacta a memoria, movendo os obxetos referenciados a posicións de memoria consecutivas, o que mellora o rendemento.
	 ![[Pasted image 20241225115722.png | center | 400]]
> Problema: as operacions de marcado e de compactación son moi ineficientes
### Estrutura
Na maioría de programas o emprego e eliminación de obxetos _non segue un comportamento uniforme_ no tempo. Para _solucionar_ esto, divídese a memoria en varias partes chamadas **xeracións**, para facilitar a xestión da vida dos obxetos:

![[Pasted image 20241225120157.png | center | 600]]

+ **Young Generation**: os _obxetos que se acaban de crear_, almacénanse e se lles asigna unha data. Consta de eden, S0 e S1.
	+ Cando se enche, lánzase unha recolección de basura menor (_RB minor_), que é moi rápida, e os obxetos que non se eliminan, pasan á xeración antiga (old generation)
+ **Old Generation**: emprégase para almacenar _obxetos de longa duración_.
	+ Na xeración nova establécese un umbral: os obxetos cunha antiguedade maior a este, pasan á xeración antiga.
	+ Cando se enche, lánzase unha recorección de basura maior (_RB major_), moito máis lenta que a RB minor.
+ **Permanent Generation**: emprégase para almacenar as clases e os métodos empregados durante a execución do programa
	+ Énchese durante a execución do programa con metadatos sobre as clases que se van empregando (_carga dinámica_)

### Funcionamento
1. A xeración nova está baleira. Cando se crea un obxeto, almacénase inicialmente no edén.
2. Cando o edén está cheo, lanzase unha RB minor: elimínanse todo o lixo, e todos os obxetos que sí son referenciados móvense ao S0. ![[Pasted image 20241225123732.png |center]]
3. Na seguinte RB minor (o edén volve a estar cheo), tanto os obxetos empregados do edén como os obxetos empregados do S0 móvense ao S1 (aumentando a súa edade); e se elimina o lixo. ![[Pasted image 20241225124035.png | center]]
4. Na seguinte RB minor, todos os obxetos empregados (tanto do edén como do S1) se moven ao S0, aumentando a súa edade; e se elimina todo o lixo.
5. Os oobxetos van pasando de S0 a S1 e viceversa en cada RB minor ata que superan o umbral de edade. Cando esto ocorre, os que o superen son promocionados á xeración antiga. ![[Pasted image 20241225124419.png |center]]
## Referencias
### Xestión avanzada
> Existe algunha forma de acceder á posición de memoria dun obxeto sobre o que se fixo aliasing?
#### Tipos de referencias
En Java existen 4 tipos de referencias según a _xestión_ que fai delas o recolector de lixo, e que _herdan da clase Reference_:
+ **Referencias fortes** (strong references):
	+ Son as referencias _por defecto_
	+ Créanse automáticamente cando se instancia un obxeto
	+ O recolctor de lixo _só as elimina cando apuntan a null_
	
+ **Referencias febles** (weak references): 
	+ Para creala, débese _instanciar a clase WeakReference_, cunha referencia á clase forte á que apunta como arg.
	+ A creación desta referencia feble non obriga ao recolector a non borrar a referencia forte á que apunta. 
	+ Para acceder á referencia forte pódese empregar o método _get_, pero non sempre ten por qué devolver unha referencia forte non nula.
	+ O recolector de lixo _elimina_ as referencias febles cando _non apuntan a unha referencia forte_ ou a referencia forte é null.
	+ Exemplo: 
		```java
		float[] rango = new float[2];
		WeakReference wrango = new WeakReference(rango);
		float[] rango2 = (float[]) wrango.get()
		// Tanto rango como rango2 apuntan á mesma dirección
		```

+ **Referencias suaves** (soft references): 
	+ Para crealas hai que instancias a clase SoftReference (igual que coa anterior)
	+ Pódese seguir accedendo á dirección de memoria á que apunta aínda que a referencia forte á que apunta fose eliminada polo recolector de lixo.
	+ O recolector só elimina estas referencias cando é estrictamente necesario dispoñer da memoria que ocupan.
	+ Exemplo: 
		```java
		float[] rango = new float[2];
		SoftReference srango = new SoftReference(rango);
		rango = null;
		float[] rango2 = (float[]) srango.get()
		//rango xa nn existe,pero rango2 segue a apuntar á dir deste
		```

+ **Referencias pantasmas** (phantom references):
	+ Para crealas, hai que instanciar a clase PhantomReference cos seguintes args: unha referencia forte á que apunta, e unha cola (instancia de ReferenceQueue) na que se almacenará dita referencia forte.
	+ Aínda que a referencia forte sexa eliminada, pódese sequir accedendo a esa dirección de memoria a través da cola (poll)
	+ O método get() devolverá sempre null, xa que este tipo de referencias están pensadas para empregarse cando a as referencias fortes xa non están dispoñibles.
	+ Exemplo:
```java
Sensor s1 = new Sensor(50, new float[]{ -10, 10 });
// Referencia fantasma
ReferenceQueue queue = new ReferenceQueue();
PhantomReference phSensor = new PhantomReference(s1.getRango(), queue);
Reference<Sensor> sensorRef = queue.poll(); // Para acceder á dir.
// Acceso a las referencias
System.out.println("Acceso a la referencia: " + sensorRef.get());
if (sensorRef != null)
	System.out.println("Referencia de s1: " + sensorRef.get());
```

#### Usos dos distintos tipos de referencias
+ As referencias **suaves** e as **pantasma** empréganse para facer _cachés en memoria_: permiten o acceso ás referencias fortes aínda que xa non estean dispoñibles en memoria.
+ As referencias **febles** empréganse para acceder _dinámicamente_ á referencia forte dun obxeto, o que _evita o aliasing_.

### Clase String
Os obxetos String pódense crear de dúas formas distintas:
+ **Directamente**: asígnase unha cadea de texto ao obxeto. A String almacénase nunha zona do montón chamada **String Pool**, polo que cada vez que se asigna a mesma cadea de texto, apúntase á dirección que a contén (no exemplo str1 e str2).
+ **Indirectamente**: o obxeto créase empregando o _constructor de String_, polo que se almacena no montón, pero _fora da String Pool_ (aínda que teña o mesmo valor que unha cadea previa) (str3).
![[Pasted image 20241225180539.png | center | 450]]

Aínda que String é unha clase, _non se comporta como o resto de clases_ na asignación entre obxetos de forma directa:
```java
String australia = "australia"; // Crease un obxeto
String continente = australia; 
String nuevoContinente = continente;
```
Neste caso só se crea un único obxeto, xa que despois `continente` e `nuevoContinente` apuntan á mesma dirección que `australia` (onde se atopa a String `"australia"`). Polo tanto, unha cadea de texto é un **obxeto inmutable**.
> Empregar excesivamente as cadeas de texto pode reducir significativamente o rendemento do programa: se unha cadea de texto se vai a modificar continuamente, deberase empregar a clase StringBuffer (xa que non se reserva memoria cada vez que se xera una string).

**==!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!==** **[[Preguntas tipo exame POO#Pregunta 2 Tema 2. Referencias| PREGUNTA DE EXAME!!!]]** **==!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!==**

## Identidade de obxetos: método equals
Considérase que **dous obxetos son iguais** nos seguintes casos:
1. **Ocupan a mesma posición de memoria**. Esta condición é _moi restrictiva_, xa que estanse comparando dúas referencias a un obxeto.
> [!Exemplo]
> Neste código `australia1` e `australia2` ocupan posicións de memoria distintas, polo que serían "obxetos distintos" .
```java
Continente australia1 = new Continente("Australia", "AZUL");
Continente australia2 = new Continente("Australia", "AZUL");
```

2. **Son do mesmo tipo e os valores dos atributos son iguais**. Esto obriga a que ambos obxetos teñan os _mesmos valores dos atributos_ e que estes sexan _inmutábeis_.
>[!Exemplo]
> Neste código, `NumEjercitos` é un atributo mutable, polo que `jugador1` e `jugador2`  só serán iguais cando `NumEjercitos` teña o mesmo valor para ambolosdous.
```java
Jugador jugador1 = new Jugador("Marta", "AZUL", 14);
Jugador jugador2 = new Jugador("Marta", "AZUL", 14); // Iguales
jugdor2.setNumEjercitos(20); // Non iguales
```

O método **equals** indica se un obxeto (pasado como arg) _é igual_ ao obxeto dende o que se invoca, e é _común a tódalas clases de Java_, que herdan a implementación de equals da clase _Object_. Esta implementación segue a _opción 1_:
```java
public boolean equals(Object obj){
	return this == obj;
}
```

Polo tanto, hai que **reimplementar** o método equals de forma que dous obxetos sexan iguais se os _atributos inmutábeis_ (normalmnte cadeas de texto ou wrappers) teñen os mesmos valores:
```java
@Override
public boolean equals(Object obj) {
	// Se a referencia é a mesma son iguais
    if (this == obj) {
        return true;
    }
    // Se o outro obxeto e null non son iguais
    if (obj == null) {
        return false;
    }
    // Se a clase é diferente non son iguais
    if (getClass() != obj.getClass()) {
        return false;
    }
    // Se os nomes ou as cores son distintas, non son iguais
    final Jugador other = (Jugador) obj;
    if (!this.nombre.equals(other.nombre)) {
        return false;
    }
    if (!this.color.equals(other.color)) {
        return false;
    }
    return true;
}
```
