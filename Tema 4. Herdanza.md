# Tema 4. Herdanza: xerarquía de clases, composición e abstracción
## Concepto de herdanza
A **herdanza** é un mecanismo mediante o cal unha _clase derivada_ reemprega os atributos e os métodos dunha _clase base_, herdándose. Ten como _obxectivo_ a construccción de clases basadas en outras clases que xa teñen implementada a funcionalidade desexada.

Os **constructores** dunha clase _non se herdan_ ás clases derivadas, xa que se consideran _específicos_ da súa clase.

Unha clase derivada considérase unha _extensión_ da clase base na que os **métodos e atributos** ou ben se herdan desta, ou se definen _explícitamente_ como propios da clase base. Entre unha clase derivada e unha clase base existe unha relación de tipo "é-un/a".

**Tipos de herdanza**:
 + _Herdanza simple_: a clase B herda todos os atributos e métodos da clase A
 + _Herdanza multinivel_: a clase C herda da clase B, que herda da clase A = clase C herda de A
 + _Herdanza xerárquica_: as clases B e C herdan de A e se diferencian nos métodos específicos 
 + _Herdanza múltiple_: a clase C herda tanto de A como de B (políticas de herdanza)
![[Pasted image 20241228102248.png | center | 200]]
**Beneficios da herdanza**:
+ Permite o _reemprego_ de código
+ _Simplifica_ o código
+ Facilita o _mantemento_ e a _extensibilidade_ dos programas

**Desvantaxes da herdanza**:
+ Código _difícil_ de entender cando o _nivel de xerarquización é moi profundo_
+ _Cambios inconsistentes_ nas clases derivadas debido a cambios nas clases base
+ Pode _comprometer a encapsulación_, xa que os atributos deben ter un modificador de acceso distinto ao privado

## Concepto de composición
A **composición** é o mecanismo mediante o cal unha clase contén obxetos doutras clases aos que se lles _delega_ certas operacións.

**Beneficios da composición**:
+ _Reparte as responsabilidades_ entre os obxetos
+ Facilita o _mantemento_ e a _extensibilidade_ dos programas
+ _As clases están desacopladas_ entre si: un cambio en unha delas ten pouco impacto nas outras

**Desvantaxes da composición**:
+ Xera moito máis código e máis complexo
+ Precisa mais tempo de desenvolveento xa que hai que impkementar os métodos en todas as clases

Dise que a composición entre dúas clases é unha relación do tipo "ten-un/a".

## Herdanza vs Composición
Cando deberíamos empregar composición en vez de herdanza?
+ Cando as clases non estean relacionadas dende un punto de vista lóxico
+ Cando unha clase base ten unha sola clase derivada
+ Cando as clsses derivadas herdan código que non precisan
+ Cando as clases poden chegar a cambiar
+ Cando hai que sobreescribir moitos métodos da clase base
![[Pasted image 20241228104455.png | center]]

## Herdanza en Java
Faise énfase en que unha clase derivada **extende** os atributos e métodos dunha clase base cunha serie de **reestriccións**: _non existe herdanza múltiple_ e só se herdan os atributos e métodos da clase base que son _públicos para a clase derivada_ (en función dos tipos de acceso).

### Revisitando os tipos de acceso
+ **Private**: a clase derivada _nunca herdará_ os atributos e métodos
+ **Public**: a clase derivada _sempre herdará_ os atributos e métodos
+ **Paquete**: a clase derivada _só herdará_ os atributos e métodos se está no mesmo paquete
+ **Protected**: a clase derivada _sempre herdará_ os atributos e métodos

Considérase que os atributos **deben ser privados**, xa que a encapsulación ten máis beneficios que a herdanza: sen encapsulación o desenvolvemento é máis dificil de _manter e validar_ e a _composición non ten sentido_. Se os atributos son _públicos_, a _encapsulación desaparece_, e se se son _protexidos_, se _debilita_.

> [!Pregunta]
> Se a clase derivada non herda os _atributos_ privados, pero sí os métodos públicos desa clase, como é posible que a clase derivada teña eses métodos públicos se non herda os atributos que son usados neses métodos?
> **Solución**: 
> En realidade, ==a clase derivada herda todos os atributos, independentemente do seu tipo de acceso, pero non se pode acceder a eles==.

> [!Pregunta]
> Se a clase derivada non herda os _métodos_ privados, pero sí os métodos públicos desa clase, como é posible que a clase derivada teña eses métodos públicos se non herda os métodos privados que son usados por eses métodos?
> **Solución**: 
> Ocorre o mesmo que no caso anterior: ==a clase derivada herda todos os métodos, independentemente do seu tipo de acceso, pero non se pode acceder a eles==.

Polo tanto, _o tipo de acceso non evita ou limita a hedanza dos métodos ou atributos_, senón que restrinxe a súa _visibilidade_.

### Constructores
Os **constructores da clase base non se herdan**, debido a que o constructor da clase base non ten acceso aos atributos da clase derivada, polo que este _non pode ser invocado_ pola clase derivada.

**Problema**: e a clase base herda todos os atributos, pero non ten acceso aos atributos da clase base, como se reserva memoria para estes atributos e se inicializan os valores apropiados?

**Solución**:
+ Se o constructor da clase base **non ten args**: cando se invoque o constructor da clase derivada, _invocarase automáticamente_ o constructor da clase base. Polo tanto, se se implementa un constructor sen args para a clase derivada, _obligatoriamente_ debe implementarse un sen args na clase base (do contrario: erro de compilación) 
+ Se o constructor da clase base **ten args**: _só se invocará a ese constructor_, xa que non podemos garantir que na clase base exista un constructor cos mesmos args. Para esto, o constructor da clase base _invócase manualmente_ con **`super`**.

==`super`==:
- Permite aos atributos, métodos e constructors da clase base dende a clase derivada, o que permite invocar a calquera constructor (sempre cando esta invocación teña lugar na primeira liña do constructor).
- Só pode acceder aos elementos da clase base inmediatamente superior á clase derivada:
![[Pasted image 20241228113027.png| center | 400]]

### Métodos e sobreescritura
A **sobreescritura** de métodos é un  mecanismo mediante o cal un método herdado dunha clase base se _implementaa novamente_ na clase derivada. É necesaria cando a implementación dun método da clase base _non é válida_ na clase derivada ou hai que _adaptala_. 
Tanto o nome do método como os seus args e o tipo que devolve deben ser os mesmos, e o tipo de acceso debe ser o mesmo ou superior.

_Todas as clases que se crean nun programa en Java son derivadas da clase Object_, polo que herdan todos os seus métodos: `finalize()` invócase cando o recolector de lixo determina que non hai mais referencias ao obxeto e o elimina, e _hai que sobreescribilo_.

Pódese empregar `super` para sobreescribir os métodos nas clases derivadas reempregando o método que está na clase base. Exemplo:
```java
public class Empleado {
    private String nombre;
    private float antiguedad;
    private ArrayList<Proyecto> proyectosParticipado;
    private float base;

    public float calcularSueldo() {
        float sueldo = this.base;
        float factor = (this.antiguedad > 15) ? 0.02f : 0.01f;
        for (int i = 0; i < this.proyectosParticipado.size(); i++) {
            sueldo += factor * this.proyectosParticipado.get(i).getPresupuesto();
        }
        return sueldo;
    }
}

public class Directivo extends Empleado {
    @Override
    public float calcularSueldo() {
        float sueldo = super.calcularSueldo(); // <----------------
        return 1.1f * sueldo;
    }
}
```


### Clases abstractas
Son clases que **non se poden instanciar**, polo que se empregan como clases _base_ de outras clases, xa qe facilitan a reutilización dos seus atributos, métodos e constructores. Estas clases poden ter _constructores_, aínda que estes só se poden invocar mediante _`super`_ (non con `new`); e _atributos e métodos_ implementados _igual_ que nas clases non abstractas. Deben _implementar_ a _maior cantidade posible de métodos_, para que as clases derivadas podan herdalos. 
> Unha clase debe ser abstracta cando nunca sexa necesario crear unha instancia desa clase

As clases abstractas poden ter **métodos abstractos**:
+ _Non teñen corpo_ (acaban sempre en ";"):
	`public abstract <tipo_dato> nome_metodo(<tipo_dato> nome*);`
+ Se unha clase ten polo menos un método abstracto, entón esta _debe ser abstracta_
+ Os métodos abstractos sempre _deben ser implemetados nas clases derivadas non abstractas_.

Unha **clase abstracta**: 
+ Pode ter todos os métodos abstractos 
		pero debería ter tantos métodos implementados como sexa posible.
+ Pode ter todos os métodos implementados
+ Pode ocupar calquera lugar na xerarquía de clases, 
		pero debería ocupar os niveis superiores
+ Pode ser unha clase derivada dunha clase non abstracta, 
		pero a súa clase base debería ser abstracta
+ Pode non ter constructores, 
		pero debería ter tantos constructores como sexa necesario
+ Pode ter atributos de calquera tipo

### Clases, atributos e métodos finais
**Estrutura típica dunha xerarquía**: clases abstractas --> clases instanciables --> clases finais
![[Pasted image 20241228144412.png | center | 600]]

As **clases finais** son clases que non permiten a creación de clases derivadas.

A palabra **`final`** en Java indica que **o elemento non se pode modificar**:
+ Se é un _método_: non poderá ser sobreescrito
+ Se é un _atributo_: unha vez toma un valor, non poderá ser modificado, polo que non _poderá ter setters_.

Os **atributos finais** empréganse para implementar as **constantes** do programa, típicamente con `final static`, para permitir _empregar a constante sen ter que instanciar a clase_, gracias a `static`, que fai que se almacene en _memoria estática_, estando dispoñible dende o principio do programa.
+ _Decalaración_: `public final static <tipo_dato> <nome_atrib> = <valor>`
+ _Uso_: `<nome_clase>.<nome_atrib>`


