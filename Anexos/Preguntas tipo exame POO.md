### Pregunta #1. Tema 2: Unboxing e Autoboxing
![[Pasted image 20241224151750.png | center | 700]]
```java
1  ArrayList<Integer> nums = new ArrayList<>();
2  Integer x = new Integer(10);
3  nums.add(10); 
4  nums.add(x); // nums = (int)10, (Integer)10
5  Integer y = nums.get(0); // y = (Integer)10 --> wrapper
6  Integer z = nums.get(1); // z = (Integer)10 --> wrapper
7  z = y; // Wrapper porque temos un arraylist de Integers
8  y = y + 10; // 
9  int res = y + 20; //
10 for (Integer val : nums) res += val; // (int)res, (Integer)val
```
###### Xustificación das respostas:
- [v] O que ocorre nesta liña, é que primeiro ocorre unboxing (`y.intValue()`) para que se poidan sumar os valores, e despois ocorre autoboxing, xa que y é un Integer.
- [ ] Falso, xa que y e z están referenciando a obxetos diferentes (`y = (Integer)10; z = (int)10`) 
- [ ] Falso, o valor de y é 20 (Integer), en cambio, z = 10  (Integer)
- [v] Verdadeiro, xa que están referenciando ao mesmo obxeto, polo que z e y apuntan á mesma dirección de memoria
- [ ] Falso, xa que se Java traduce o `val` automaticamente a `val.intValue()`
- [v] Verdadeiro, xa que se está convertindo un obxeto wrapper (`y`) a un tipo primitivo (`res`)

### Pregunta #2. Tema 2: Referencias
![[Pasted image 20241225185715.png | center | 700]]
```java
1  ArrayList<Coche> coches = new ArrayList<>();
2  coches.add(new Coche("0000 ABC"));
3  coches.add(new Coche("0001 DEF"));
4  coches.add(new Coche("0002 HIJ"));
5  coches.add(new Coche("0004 KLM"));

6  Coche coche1 = coches.get(3); // Non se reserva memoria (punteiro)
7  String mat3 = coche1.getMatricula(); // Non se reserva memoria
8  mat3 = "0003 HIJ"; // Reserva de memoria (StringPool)

9  for(int i = 0; i < coches.size(); i++) {
10     if(i == 3) coches.remove(i); // eliminase o coche1
11     else {
12         String mensaje = "Coche no eliminado";
13         System.out.println(coches.get(i).getMatricula());
14     }
15 }
```
> Nota: nas liñas 2-5 os obxetos Coche almacenanse no heap e o seu atributo Matricula apunta ás Strings "0000 ABC", "0001 DEF"..., almacenadas na StringPool.
###### Xustificación das respostas:
 - [v] Verdadeiro, xa que ao facer a asignación da liña 8, mat3 apunta a outra rexiom de memoria, pero a matrícula do último coche non se modifica debido a que se trata dunha String.
 - [ ] Falso, debido a que a `mat3` se lle asigna unha copia da referencia á cadea.
 - [v] Verdadeiro, xa que tanto `coche1` como `coches.get(3)` apuntan agora á mesma dirección de memoria
 - [ ] Falso, debido a que se realiza unha reserva de memoria para `mensaje` en cada iteración, pero `coches.get(i).getMatricula()` non reserva memoria porque as strings xa existen.
 - [ ] Falso, só se reserva memoria na liña 8; nas liñas 6 e 7 só se involucran referencias
 - [ ] Falso, xa que primeiro se accede ao dato e despois se elimina, xusto cando remata o bucle.

### Pregunta #3. Tema 3: HashMaps
![[Pasted image 20250104145638.png]]
###### Xustificación das respostas:
- [ ] Falso, xa que se hai moitos obxetos coa mesma clave (hai moitas colisións), o acceso aos datos pode verse afectado
- [ ] Falso. Os HashMaps son coleccións, pero non porque os obxetos non se almacenan na orde na que se van introducindo, senon porque implementan a interfaz Map.
- [v] Verdadeiro, xa que todas as colleccións producen iteradores; neste caso `entrySet`, `keySet` ou `values`.
- [v] Verdadeiro. Cando se invoca o método `get(cla1)`:
	1. Calcúlase o hashCode da clave `cla1`
	2. Itérase sobre todas as entradas que teñan ese hashCode e compara as claves almacenadas con `cla1`, empregando o método `equals`.
	3. Se o `equals` devolve true, devolve ese obxeto
- [ ]  Falso, xa que primeiro se deben comparar as claves con `equals` xa uqe varios obxetos poden ter o mesmo hashCode.
- [ ] Falso, xa que malia que nalgunhas implementacións se permita almacenar datos nulos, non se permite o almacenamento de datos repetidos, xa que as claves deben de ser únicas.

### Pregunta #4. Tema 5: Upcasting
**Que é o upcasting? Xera erros? Xustifica a túa resposta** 
###### Resposta
O upcasting ocorre cando un obxeto dunha clase derivada se comporta como un obxeto da clase base, e nunca xerará erros xa que a herdanza obriga a que as clases derivadas teñan os mesmos atributos que as clases base.

### Pregunta #5. Tema 5: Downcasting
**Que é o downcasting? Xera erros? Xustifica a túa resposta**
###### Resposta
O downcasting ocorre cando se forza a un obxeto dunha clase base a actuar como un obxeto dunha das súas clases derivadas. Pode xerar erros con moita facilidade xa que non hai garantías de que a clase derivada teña os mesmos atributos que a clase base, polo que se considera unha opción unsafe e normalmente se emprega só para desfacer un upcasting.

### Pregunta #6. Tema 4: Herdanza
**Explica o concepto de herdanza.**
###### Resposta


### Pregunta #7. Código
**Clase Hospital**:
Tiene los siguientes atributos:
- **nombre**: `String nombre`
- **coste por día del hospital**: `double costeDiaHospital`
- **provincia en la que se encuentra**: `String provincia`
- **conjunto de pacientes que están ingresados en el hospital**: `HashMap<String,Paciente> pacientes`
- **presupuesto del hospital**: `double presupuesto`
- **número de días acumulados**: `int numeroDiasAcumulados`
- Todos los atributos tienen los modificadores de acceso de tal modo que se favorezca la encapsulación.
- Todos los atributos tienen los métodos de escritura (setter) y lectura (getter).
- Tiene un constructor sin argumentos en el que se inicializan los atributos a sus valores por defecto.
- Tiene un constructor cuyos argumentos son el nombre, la provincia y el coste por día.

**Clase Paciente**:
Tiene los siguientes atributos:
- **nombre**: `String nombre`
- **enfermedades que sufre el paciente**: `ArrayList<String> enfermedades`
- **hospitales en los que ha estado ingresado**: `ArrayList<Hospital> hospitalesIngresado`
- **número de días que ha estado ingresado en cada hospital**: `HashMap<String,Integer> numeroDias`
- Todos los atributos tienen los modificadores de acceso de tal modo que se favorezca la encapsulación.
- Todos los atributos tienen los métodos de escritura (setter) y lectura (getter).
- Tiene un constructor sin argumentos en el que se inicializan los atributos a sus valores por defecto.
- Tiene un constructor cuyos argumentos son el nombre del paciente y el conjunto de enfermedades que sufre el paciente.

**PREGUNTA 1 (1,50 PUNTOS)**
En la clase **Paciente**, crear un método llamado **existePacienteMasGrave** que devuelva si existe algún paciente (i) que haya estado ingresado en alguno de los hospitales en los que ha estado ingresado el paciente; y (ii) que en ese hospital haya estado ingresado más días que el paciente.
**Nota 1**: Se deberá recorrer los **HashMap** con un **for-each** a partir de sus valores. (0 puntos si no es así)
###### Resposta



