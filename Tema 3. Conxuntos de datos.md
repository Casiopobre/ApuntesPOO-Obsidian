# Tema 3. Conxuntos de datos: arrays, coleccións, listas, conxuntos e mapas
Ao programar manexanse conxuntos de datos sobre os que se realizan _operacións CRUD_ (create, read, update and delete), e, malia que a maioría das linguaxes de programación permiten empregar _arrays_ para rerpresentar conxuntos de datos, estes teñen moitas _limitacións_, polo que _Java soporta directamente varios tipos de conxuntos de datos_.
> Todos os tipos de conxuntos de datos son mapas, coleccións ou iteradores; os outros tipos de conxuntos de datos particularizan os anteriores (ex: ArrayList ou HashMap) ![[Pasted image 20241227104928.png | center | 400]]
## Arrays
É un _conxunto de elementos do mesmo tipo que ocupan posicións consecutivas de memoria_. 
+ Dado que en Java é un **obxeto**, débese empregar _new para reservarlle memoria_ e herda todos os métodos de _Object_ , ademáis de ter a súa _lonxitude como atributo público_ (length).
+ ==Os arrays son as **únicas estruturas que permiten almacenar tipos de datos primitivos**.==
+ **Accédese** aos elementos do array mediante un _índice_ (dende 0 a length-1) e se se intenta acceder a unha posición > length-1, xérase un erro: _ArrayIndexOutOfBoundException_
+ **Limitacións**: _tamaño fixo_ e imposibilidade de _borrar_ datos cando son tipos primitivos (debido a que en datos primitivos non se pode empregar null, polo que non existe un valor por defecto).
```java
int[] numExercitos = new int[6]; // Tamaño do array = 6 (fixo)
// Acceso a través do índice
for(int i = 0; i < numExercitos.length; i++)
	numExercitos[i] = 14 + i;
// Borrado dun dato en un array de obxetos:
String[] cores = {"Amarelo", "Vermello", "Rosa", "Violeta"}
// Despois do borrado de "Vermello":
String[] cores = {"Amarelo", null, "Rosa", "Violeta"}
```

## Coleccións
### Collection
As coleccións son _grupos ou conxuntos de datos ou elementos_ sobre os que se definen _operacións de inserción, borrado ou actualización_. **Collection** é unha _interface_ que define as operacións que debe ter unha colección, e non se lle pode reservar memoria a un obxeto de tipo Collection xa que _non é unha clase_. Ademáis, **non se pode recorrer** unha colección a través dun índice debido a que non é un grupo ordeado de elementos.
![[Pasted image 20241227110221.png | center | 250]]

**Métodos de Collection**: 
+ `boolean add(E ele)`: _engade_ o elemento `ele` á colección
+ `boolean contains(Object obj)`: _comproba_ se o obxeto `obj` está na colección
+ `boolean isEmpty()`: indica se unha colección está _baleira_
+ `void remove(Object obj)`: _elimina_ o obxeto `obj` da colección
+ `Iterator<E> iterator()`: xera un _iterador_ para poder recorrer a colección
> Os métodos `contains` e `remove` empregan `equals` para a comprobación.

Se a implementación de Collection non soporta algún dos seus métodos, xerarase unha excepción _UnsupportedOperationException_.
> [!Exemplo]
> O método `values()` da clase HashMap devolve unha Collection cuxo método para engadir elementos (`add`) non está soportado (xa que non queremos que se modifique a colección). Polo tanto é necesario implementar `add`, xa que a clase ten que implementar todos os métodos de collection:
```java
public boolean add(E e){
	throw new UnsupportedOperationException();
}
```

Para **recorrer** unha colección pódese empregar un bucle **`for-each`**:
```java
Collection<Continente> colContinentes = this.continentes.values();
for(Continente continente : colContinentes)
	System.out.println("Nombre: " + continente);
```
Neste caso, `colContinentes` é unha colección xerada polo método `values()` da clase HashMap, e que se recorrerá no bucle for-each; e `continente` é  o obxeto que se extrae da colección en cada iteración.

As coleccións **non se poden modificar** mentres se recorren: ConcurrentModificationException.
```java
public Collection borrarContinente(Continente aBorrar) {
    Collection<Continente> colConts = continentes.values();
    for (Continente continente : colConts) {
        if (continente.equals(aBorrar)) {
            colConts.remove(aBorrar);
        }
    }
    return colConts;
}
```
Neste caso se a clase `Continente` non reimplementa `equals()`, _`remove()` compara a referencia_ do arg `aBorrar` coa dos elementos da colección, polo que na maioría dos casos _non atopará o obxeto_.

### Iterator
É unha _intereface_ na que se definen un conxunto de _operacións para recorrer os elementos_ dunha colección. Para esto, emprégase un _punteiro ou iterador_ que sinala ao seguinte elemento.

**Operacións básicas (métodos de Iterator)**:
+ `boolean hasNext()`: _indica se existe_ un elemento na pos. de mem. contigua á do punteiro
+ `E next()`: obtén o elemento da posición contigua e _actualiza_ o punteiro a esta posición
+ `remove()`: _elimina_ o elemento que está na posición actual

É unha _forma alternativa ao for-each_, polo qu presenta varias **diferencias** con este:
+ _Permite a eliminación_ dos elementos mentres se recorre a colección: elimina tanto os elementos da colección como do iterador
+ Só se pode _empregar unha única vez_ (cando chega ao final `hasNext() = false`)
+ O _rendemento é o mesmo_, xa que o compilador interpreta un for-each como se fose un iterador.

```java
public Collection borrarContinente(Continente aBorrar) {
    Collection<Continente> colConts = continentes.values();
    Iterator<Continente> itConts = colConts.iterator();
    while(itConts.hasNext()) {
        Continente continente = itConts.next();
        if(continente.equals(aBorrar)) {
            itConts.remove();
        }
    }
    return colConts;
}
```
Ao invocar a `itConts.remove()` non ocorre ningún erro, porque o valor do punteiro actualízase ao valor que tiña antes da chamada a `next()`, que obtén tanto o obxeto actual, como o seguinte. 

## Listas
### List
Son coleccións nas que _os elementos teñen unha orde_, determinada pola secuencia mediante a que foron engadidos os elementos, e que _sempre se mantén_ gracias a que a cada elemento se lle asigna un **índice**.
![[Pasted image 20241227131637.png | center | 250]]

Así, unha lista pódese _recorrer empregando un índice_ ou mediante un _for-each_; e tamén pode conter **elementos duplicados**.

**Métodos de List**:
+ `E get(int i)`: obtén o obxeto que se atopa na posición `i`.
+ `void set(int i, E ele)`: actualiza o obxeto da posición `i`.
+ `E remove(int i)`: elimina o obxeto da posición `i`.

### ArrayList
É un tipo de lista que soporta a **redimensión dinámica** cando o número de datos a almacenar é maior que a capacidade da lista. Esta rediemensión é _automática_, pero se se realiza con moita frecuencia pode _reducir o rendemento_ (debido a que implica incrementar o tamaño dun array de obxetos mediante unha operación de caché de datos (Arrays.copyOf)).

O **constructor** sen args _reserva espazo para 10 elementos_: diferénciase entre o _tamaño_ do conxunto de datos que se quere meter e a _capacidade_ da lista; e cando a lista alcanza o seu _límite_ de capacidade, por defecto _aumenta_ esta _en 10 obxetos_.

Se **percorremos** a lista a través do índice, _pódese modificar o seu contido_, e ademáis será necesario comprobar que os obxetos almacenados sexan _distintos de null_ (xa que un obxeto de ArrayList pode _conter obxetos de tipo null_).

A clase ArrayList **encapsula un array de obxetos** ao que se pode acceder mediante métodos definidos na interface List: a _referencia_ ao array almacénase na _pila_, mentres que o _array_ e os outros _atributos_ da clase se almacenan no _montón_. ![[Pasted image 20241227151606.png | center | 350]]
As operacións de acceso aos obxetos do ArrayList teñen un **tempo lineal** ($O(n)$)

**Aliasing**: ten un maior impacto ao empregar conxuntos de datos, xa que permite modificar os seus elemetnos sen cambiar a dirección:
```java
ArrayList<ArrayList<Casilla>> casillas = mapa.getCasillas();
Casilla casilla = casillas.get(0).get(7); // Aliasing
Pais pais = casilla.getPais();
pais.setNombre("Antártida");
```

## Conxuntos
### Set
Os conxuntos son **coleccións nas que non se poden repetir os datos**.
![[Pasted image 20241227153237.png | center | 250]]

**Set** é unha interface na que se definen as mesmas operacións que nunha _Collection_, e son as _implementacións_ as que se encargan de que se cumpla a condición de desiguadade entre obxetos:
```java
Object e1, e2;
if(!e1.equals(e2)) return true;
```
>Polo tanto, nun Set pode haber, como moito, un único null.

Ao ser unha colección, emprégase un _iterador ou un for-each_ para percorrer o Set, e é necesario _sobreescribir_ o método _`equals()`_ das clases dos obxetos do conxunto. 

Non se pode permitir modificar un obxeto de froma que este vaia ser igual a outro obxeto do Set (esto pode ocorrer cando as modificacións non se realizan cos métodos de Set):
> [!Exemplo]
> En `conjuntoPaises` o criterio de identidade é o nome do país, no segundo bucle, se hai un nome de país que se chame "Siberia", cambiaselle o nome por "Rusia": _hai dous países iguais e non se xeran erros_ (pq empregamos un método da clase `Pais`).
```java
System.out.println("Países antes de modificación");
for(Pais pais : conjuntoPaises)
    System.out.println(pais.getNombre()); 
// Paises: Siberia, GBretaña, Rusia

System.out.println("Países después de modificación");
for(Pais pais : conjuntoPaises) {
    if(pais.getNombre().equals("Siberia"))
        pais.setNombre("Rusia");
    System.out.println(pais.getNombre());
} // Paises: Rusia, GBretaña, Rusia
```
### HashSet
É un **wrapper da clase HashMap** que implementa a interface Set, polo que _internamente os datos se almacenan como as claves dun obxeto HashMap_. Así, non se asegura que os datos se garden na _orde_ na que foron insertados, xa que esta orde está basada no seu _hash code_. Gracias a esto, as operacións de acceso ocorren nun _tempo constante_ ($O(1)$).
![[Pasted image 20241227212727.png | center | 250]]
## Mapas
### Map
É unha interface que **realciona unha clave cun valor**, polo que, _a partitres da clave se obtén o valor asociado a esta_. 
**Características**:
+ As claves e os valores son _obxetos_ (non poden ser tipos primitivos)
+ As claves non se poden repetir pero os obxetos si (_varias claves poden ter asociado o mesmo valor_)
+ En algunhas implementacións pódense almacenar claves e valores _nulos_.

A **clave** dun mapa pode ser calquera tipo de obxeto:
+ Emprégase _equals_ para localizar e obter a clave coa que se recuperará o valor, polo que deberá sobreescribirse cun criterio de igualdade específico.
+ A clave debe ser un _obxeto inmutable_.
+ Algúnhas implementacións non soportan todos os métodos de Map, xerando unha excepción (_UnsupportedOperationException_)

**Métodos de Map**:
+ `V get(Object key)`: _devolve_ o valor asociado á clave `key`
+ `V put(K key, V value)`: _almacena_ un valor asociado a unha clave
+ `boolean containsValue(Object value)`: indica se un valor _está no mapa_ (se ten asociada unha clave)
+ `boolean containsKey(Object key)`: indica se _existe alǵun dato asociado á clave_ `key`
+ `V remove(Object key)`: _elimina_ a clave e o valor asociado a partires da clave `key`
+ Métodos que _convirten_ as claves e coleccións a coleccións ou conxuntos:
	+ `Collection<V> values()`: devolve unha _colección_ cos _valores_ do mapa
	+ `Set<K> keySet()`: devolve un _conxunto_ coas _claves_ do mapa
	+ `Set<Map.Entry<K, v>> entrySet`: devolve un _conxunto_ con todas as tuplas _clave-valor_ do mapa

Os obxetos almacenados nun mapa **non se poden recorrer directamente**, polo que se quixesemos recorrer un Map, por exemplo: 
```java
private void generarPaises() {
    Set<String> setContinentes = continentes.keySet(); // Colección
    for (String claveCon : setContinentes) {
        Continente continente = continentes.get(claveCon);
        System.out.println("Añadir países de continente " + continente);
        for (Pais paisContinente : continente.getPaises()) {
            paises.put(paisContinente.getAbreviatura(), paisContinente);
        }
    }
}
```
Aquí, `continentes` é un `Map<String, Continente>`, polo que se emprega `keySet()` para xerar un _conxunto de claves que se recorren cun for-each_.

**Map.Entry** é unha interface que define métodos pra poder acceder  á dupla clave-valor:
+ `K getKey()`: para acceder á clave da entrada no mapa
+ `V getValue()`: para acceder ao valor da entrada no mapa
```java
private void generarPaises() {
    Set<Map.Entry<String, Continente>> meCont = continentes.entrySet();
    for (Map.Entry entrada : meCont) {
        Continente continente = (Continente) entrada.getValue();
        System.out.println("Añadir países de continente " + continente);
        for (Pais paisContinente : continente.getPaises())
            paises.put(paisContinente.getAbreviatura(), paisContinente);
    }
}
```
> Emprégase `entrySet()` para acceder ao conxunto de entradas do HashMap (permite obter a clave ou o dato)

### HashMap
É unha clase que implementa a interface Map na que **as claves do mapa están asociadas a un código hash** que se emprega para _comprobar se dúas claves son iguais_ (complementando o método equals), polo que cando se comparan dous obxetos nun HashMap ou HashSet emprégase o seguinte _procedemento_:
1. Compróbase se os obxetos teñen o mesmo _hash code_
2. Se o hash code é igual, invócase a _equals_

Asúmse que dous obxetos distintos poden ten o mesmo hash code.

O emprego do hash code simplifica e fai máis eficiente o acceso aos datos dun HashMap, xa que en primeira instancia emprégase a comparación de enteiros. Para xerar o hash code, hai que sobrescribir o método `hashCode()` herdado de Object (método nativo).

## Comparativa dos conxuntos de datos

![[Pasted image 20241227233353.png | center | 500]]

As _listas_ ocupan menos memoria que os _mapas_ pero estes son máis rápidos que as listas.

