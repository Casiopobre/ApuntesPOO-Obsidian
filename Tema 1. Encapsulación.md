# Tema 1. Encapsulación: tipos de datos, clases e obxetos
## 1. Tipos de datos
Programa: serie de instruccións que operan sobre una conxunto de datos (entrada) e xeran outro conxunto de datos (saída).
Teorema de Jacopini: coas instruccións de selección e de repetición pódese crear calquera programa.
A idea máis importante na Programación Orientada a Obxetos é que ==todos os tipos de datos son clases e, polo tanto, todos os datos son obxetos==
## 2. Encapsulación
Serve para **asegurar a intergridade dos datos**: limita o acceso a algúns datos dende distintos trozos do programa. *Por exemplo, idealmente os atributos dunha clase só poden ser accesibles por métodos desa clase*. Para esto, emprega o **principio de ocultación**.
## 3. Clases
Os tipos de datos son as entidades que se queren representar no programa e se conceptualizan como **clases**. Os valores concretos desas clases denomínanse **obxetos**.

En POO distínguense dúas especies de tipos de datos:
- *Tipos de datos primitivos*: están vinculados á representación de datos no ordenador (son os mesmos tipos de datos que ten C)
- *Clases*: son tipos de datos vinculados ás entidades de alto nivel do programa (non se poden representr de forma directa no ordenador)

Á súa vez, as clases conteñen dúas clases de código:
- As variables ou *atributos*: son as características que definen á entidade representada
- As funcións ou *métodos*: acceden aos atributos para permitir a súa consulta e actualización e para proporcionar as funcionalidades requeridas ao programa

[[Exemplo estrutura clase|Estrutura xeral dunha clase:]] [^1]
![[Pasted image 20241223161816.png]]

[^1]: [[Erros típicos de programación]]

### Tipos de acceso
En java, hai 4 tipos de acceso, aplicables tanto a métodos como a atributos:
* _Público_(`public`): accesibles dende calquera parte do código
* _Privado_(`private`): só son accesibles dende métodos da propia clase, polo que pra acceder a atributos privados dende outra clase hai que empregar os **getters e setters**.
* _Acceso a paquete_ (` `): únicamente accesibles mediante métodos do mesmo paquete (herdanza de clases)
* _Protexido_(`protected`): accesibles mediante métodos do mesmo paquete e métodos das subclases (aínda que estean noutro paquete). Facilita a herdanza de atributos.

### Métodos
#### Getters
Devolven o valor que teñen os atributos en cada momento.
* Cada atributo da clase ten **un único getter**.
* O nome do getter e get + <nome_atributo> en camelCase (**`getAtributo`**)
* Normalmente só consisten na devolución do valor do atributo (**`return valor_atributo`**)
#### Setters
Escriben o valor dos atributos.
* Cada atributo da clase ten **un único setter**.
* O nome do setter e set + <nome_atributo> en camelCase (**`setAtributo`**)
* Normalmente **comproban certas condicións** sobre os valores que pode adquirir o atributo para poder manter a integridade dos datos.
#### Constructores
 > A _declaración dun atributo_ dunha clase (a.k.a. dunha variable) ten distintos efectos según o seu tipo de dato: se é un tipo de dato primitivo, resérvase memoria automáticamente; pero _se é de tipo clase, non se lle fai unha reserva de memoria automática_, polo que se lle asigna un valor inicial de `null`, o que pode provocar unha `NullPointerException` se se intenta usar (xa que na práctica, a variable se trat como se non existise). 
 > Para solucionar esto, faise unha _reserva de memoria manual_ para cada atributo de tipo clase: invócanse os constructores a través do operador new.

Un **constructor** é un método que se invoca para:
* Reservar memoria para un **obxeto** da clase
* Reservar memoria para os _atributos_ de dito obxeto
* Asignar _valores iniciais_ aos atributos do obxeto

Un constructor _non devolve ningún tipo de dato_ e _o seu nome coincide co nome da clase_ á que pertence. Invócase _unha única vez para cada obxeto_, xa que en realidade, cando se reserva memoria para un obxeto, o nome do mesmo é unha **referencia á posición de memoria** na que se almacenan os datos do obxeto. Polo tanto, _se volvemos a invocar ao constructor_, apuntarase a unha **nova dirección de memoria**.

Java proporciona un **constructor por defecto**, que non ten argumentos e inicializa os atributos ao seu valor por defecto (é o mesmo que especificar un costructor sen argumentos e co corpo baleiro: `public Constructor(){}`).
#### Métodos funcionais
Acceden **directamente** aos valores dos atributos da clase e se crean cando _os datos necesarios para realizar as operacións_ son os valores dos atributos de dita clase. Os métodos **invócanse dende os obxetos** das clases.

Un método pode ter varias implementacións: **método sobrecargado**.
+ O _nome_ do método é o _mesmo_ en todas as implementacións
+ Os _tipos de args son distintos_
+ _O obxetivo do método ten que ser o mesmo en todas as implementacións_
+ É mala práctica empregar condicións sobre os argumentos para seleccionar o trozo de código que se ten que executar en cada caso
#### Método toString
Devolve a **representación en texto** dun obxeto dunha clase, e é _común a todas as clases de Java_ (herdan a implementación do toString que ten a clase Object²). Esta implementación herdada é moi _xenérica_ e non aporta información sobre o contido do obxeto (xa que śo se compón do nome da clase á que pertenceo obxeto e un código hash que o identifica³, polo que é necesario **reimplementar** o toString para obter unha representación adecuada á clase (`@Override`).
²A clase que está no nivel mais alto da xerarquía de Java
³O toString xenérico:
```java
public String toString(){
	return getClass().getName() + '@' + Integer.toHexString(hashCode());
}
```

## Rexistros
É unha clase cuxas instancias son inmutábeis⁴ (non se poden cambiar os valores dos atributos en tempo de execución). Restriccións:
+ Todos os seus **atributos son privados**
+ Todo atributo **ten o seu getter**
+ Os atributos **non teñen setters**
+ Teñen un **constructor canónico** cos seus args correspondentes par cada un dos atributos
+ O _toString_ inclúe o nome da clase e o nome dos atributos cos seus correspondentes valores
⁴Os valores dos atributos especifícanse no constructor.

Pódese reimplementar o costructor canónico sempre que se especifiquen todos os args ou se empregue unha _declaración compacta_, pódense engadir construtores sempre que chamen ao constructor canónico do rexistro, e se poden introducir métodos funcionais sempre que non modifiquen o valor dos atributos:
```java
public record Continente(Arraylist<Pais> paises, String nombre){
	// Declaracion compacta 
	public Continente {
		Objects.requireNonNull(paises);
		Objects.requireNonNull(nombre);
	}
	// Novo constructor (debe invocar ao canónico)
	public Continente(ArrayList<Pais> paises){
		this(paises, "Asia");
	} 
	// Método funcional (non pode escribir sobre os atributos)
	public boolean eGrande(){
		if(paises.size() > 10)
			return true;
		return false;
	}
}
```

## Execución dun programa en Java
Todos os programas en Java teñen unha **clase principal**, na que se atopa o método main, que é o punto a partir do cal se inicia a execución do programa. Normalmente, _no main créanse un ou varios obxetos a través dos seus constructores_, que executan as distintas partes do programa. Ademáis, o main adoita ter _poucas liñas de código_ e ==a clase principal non debe ter ningún atributo==.
