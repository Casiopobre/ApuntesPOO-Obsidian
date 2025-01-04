### Pregunta #1 : Tema 2. Unboxing e Autoboxing
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

### Pregunta #2 : Tema 2. Referencias
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

