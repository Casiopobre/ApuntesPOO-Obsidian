# Tema 7. Excepcións: xestión de erros e excepcións
## Concepto de excepción
A **xestión de erros** é unha das tareas máis importantes no desenvolvemento dun programa.
Na programación dos métodos débese favorecer a _separación lóxica_ dos distintos tipos de código (código asociado: á funcionalidade, á interacción, ao almacenamento e á xestión de erros)

Un erro pódese tratar en distintos **lugares** do código:
+ No _método que detecta o erro_: o código do método vermello encárgasede todo e o do verde só ten que invocar ao vermello.
![[Pasted image 20250102171150.png | center | 300]]

+ No _método que chama_ ao método que detecta o erro: o método vermello só se encarga de detectar o erro, e este trátase no método verde, o que simplifica o código.
![[Pasted image 20250102171356.png | center | 300]]

+ _Separando_ os tipo de código: o erro detéctase no vermello e o tratamento deste faise no verde, pero cunha clara separación entre o código que trata o erro e o código que lle outorga a funcionalidade ao método; polo que un cambio en un dos tipos de código non afectaría ao outro.
![[Pasted image 20250102171645.png | center | 300]]

Unha **excepción** xérase cando ocorren erros ou situacións de interés _durante a execución_ dos métodos. Ademáis de estar relacionadas cos erros, tamén resolven _situacións_ que se deben tratar e que forman _parte da lóxica do programa_. 

En Java, para tratar excepcións, _sepárase o código_ para a detección, a comunicación e o tratamento das excepcións:
![[Pasted image 20250102173246.png | center | 300]]
1. O método verde _intenta_ executar o seu código
2. O método vermello _detecta e xera_ unha excepción, e llo comunica ao método verde
3. O método verde _captura e trata_ o erro a parte do código funcional

## Definición de excepcións
Unha excepción é unha clase derivada da clase **`Throwable`**, cos seguintes métodos principais:
+ `String getMessage()`: devolve a mensaxe que se manda cando ocorre a excepción
+ `void printStackTrace()`: imprime en consola a secuencia de invocacións de métodos que levaron a que ocorrese a excepción

**Tipos de excepcións**:
+ _Excepcións chequeadas_ (checked): compóbase en tempo de compilación en qué métodos pode ocorrer unha excepción. Eses métodos teñen que _indicar de forma explícita_ esa posible ocorrencia. Son clases _derivadas da clase `Exception`_
+ _Excepcións non chequeadas_ (unchecked): non se comproba en tempo de compilación en qué métodos pode ocorrer unha excepción, polo que é _o programador quen debe chequealo_. Son _clases derivadas de `RuntimeException` ou `Error`_.
Se o erro que provoca que ocorra a excepción _non impide a execución do programa_, a excepción debe ser _chequeada_.

Definir excepcións como **clases derivadas de `Exception`** outorga máis control sobre a xestion destas, xa que os métodos están obrigados a declarar que excepcións poden ocorrer na sua invocación. _Constructor_: `public Exception(String message)` (debe ser invocado dende a clase derivada de Exception)

Nas **excepcións chequeadas** o compilador obriga a que se indiquen _explicitamente_ os métodos nos que teñen lugar ditas excepcións:
+ Débense _etiquetar_ os métodos onde teñen lugar as excepcións
+ Un mesmo método pode estar etiquetado con _máis dun tipo de excepción_
+ Un _constructor tamén pode xerar excepcións_: 
	+ `<tipo_acceso> <tipo_dato> nome_metodo(<args>*) throws <excepcion>`
	+ `tipo_acceso> nome_clase(<args>*) throws <excepcion>`

Na declaración do método se deben **especificar todas as excepcións** que poderían ocorrer, aínda que se todas estas pertencen á _mesma xerarquía_, sería suficiente con especificar a _excepción base_.

## Xestión de excepcións
### 1. Try
Un **método A intenta executar o método B**: hai que indicar en qué parte do gódigo do método A se vai intentar a execución do método B. No _bloque try_ se debe _invocar obrigatoriamente ao método B_ (ainda que o ideal é que todo o código funcional do método A estea dentro dun único try).
>[!Exemplo]
> Como o método `setSueldo` pode xerar unha excepción do tipo `SueldoMinimo`, este método debe invocarse dende un try.
```java
public static void main(String[] args) {
    try {
        Empresa empresa = new Empresa("MiEmpresa");
        Empleado empleadoB1 = new Empleado("EmpleadoB1");
        Empleado empleadoD1 = new Empleado("EmpleadoD1");
        Empleado empleadoP = new Empleado("EmpleadoP1");

        empresa.getEmpleados().add(empleadoB1);
        empresa.getEmpleados().add(empleadoD1);
        empresa.getEmpleados().add(empleadoP);

        for (Empleado empdo : empresa.getEmpleados()) {
            empdo.setSueldo(empdo.calcularSueldo() / 1.05f);
        }
    } catch (SueldoMinimo sm) {
        System.out.println("Error -> " + sm.getMessage());
    } catch (SueldoMaximo sm) {
        System.out.println("Error -> " + sm.getMessage());
    }
}
```

### 2. Throw
Cando se invoca ao **método B**, o seu código ten **2 partes**:
1. _Detectar_ a excepción: consiste en especificar dentro do código as condicións nas cales se xera a excepción.
2. _Lanzar_ a excepción: consiste en _crear un obxeto do tipo de excepción_ que se transferirá ao trozo de código no que se trata a excepción en cuestión. Cando se crea un obxeto do tipo de excepción, normalmente inclúese información sobre o _contexto_ no que ocurriu. Ao lanzar unha excepción _se interrope a execución do método_.
```java
if(<condicion>){
	<tipo_excepcion> <nome_obxeto> = new <constructor>;
	throw <nome_obxeto>;
}
```

A execución do programa _párase_ ao chegar ao `throw` e _continúa nese punto_ tamén. 
A información do _contexto_ no que ocorreu a excepción pásase _nos args do constructor_ da clase asociada á excepción.
```java
public void setSueldo(float sueldo) throws SueldoMinimo, SueldoMaximo {
    // (1) DETECTAR LA EXCEPCIÓN
    if (sueldo < 950) {
        // (2) GENERAR LA EXCEPCIÓN "SueldoMinimo"
        String mensaje = "El sueldo " + sueldo + " es menor que el mínimo";
        SueldoMinimo error = new SueldoMinimo(mensaje, this);
        throw error; // LANZAR LA EXCEPCIÓN A TRAVÉS DE "throw"
    } else if (sueldo > 5000) {
        // (2) GENERAR LA EXCEPCIÓN "SueldoMaximo"
        String mensaje = "El sueldo " + sueldo + " es mayor que el máximo";
        SueldoMaximo error = new SueldoMaximo(mensaje, this);
        throw error; // LANZAR LA EXCEPCIÓN A TRAVÉS DE "throw"
    }
    this.sueldo = sueldo;
}
```

### 3. Catch
Unha vez lanzada a excepción, esta se transfire como "arg" ao código no que se trata (**captura da excepción**). Normalmente este tratamento consiste en mostrar un _mensaxe de texto_ que se pasou como arg ao constructor da excepción; e ten lugar nos **bloques `catch`**, que están asociados aos `try` (==non pode haber `catch` sen `try`==)
```java
try{
	// Código
} catch(<tipo_excepcion> <nome_excepcion>){
	// Tratamento da excepción 
}
```

**Restriccións nos bloques try-catch**:
+ Para cada `catch` debe haber _un único `try`_.
+ Cada `try` ten que ter asociado, _polo menos_, un bloque `catch`.
+ O `try` _pode ter tantos_  `catch` _como_ tipos de excepciones que poida lanzar o `try`.
+ O `try` _pode ter menos_ `catch` _que_ o número de excepcións que se lancen no `try`, xa que se as excepcións teñen a mesma clase base, pode definirse _un único `catch`_, e se o tratamento é o mesmo pode empregarse un _multi-catch_.
```java
public static void main(String[] args) {
    try {
        Empresa empresa = new Empresa("MiEmpresa");
        Empleado empleadoB1 = new Empleado("EmpleadoB1");
        Empleado empleadoD1 = new Empleado("EmpleadoD1");
        Empleado empleadoP = new Empleado("EmpleadoP1");

        empresa.getEmpleados().add(empleadoB1);
        empresa.getEmpleados().add(empleadoD1);
        empresa.getEmpleados().add(empleadoP);

        for (Empleado empdo : empresa.getEmpleados()) {
            empdo.setSueldo(empdo.calcularSueldo() / 1.05f);
        }
    } catch (SueldoMinimo sm) { // CATCH #1
        System.out.println("Error -> " + sm.getMessage());
    } catch (SueldoMaximo sm) { // CATCH #2
        System.out.println("Error -> " + sm.getMessage());
    }
}
```
Podería empregarse un **multi-catch** para simplificar o código:
`catch(<tipo_excepcion> | <tipo_excepcion> | * <nome_excepcion>)`
```java
} catch(SueldoMinimo | SueldoMaximo sm){
	System.out.println("Error -> " + sm.getMessage());
}
```

**Papel da herdanza e do polimorfismo**: 
Se nun bloque catch se captura unha excepción das clases superiores a unha clase A, entón despois dese catch non pode existir outro catch que capture a clase A, xa que esta excepción xa se capturou no catch superior: _erro de compilación_
![[Pasted image 20250104123307.png | center | 600]]

**Bloque `finally`**: _execútase sempre_, independentemente de se se capturou ou non a excepción, e emprégase habitualmente para _liberar recursos_.
+ Cada try pode ter coma moito un _único_ finally
+ O finally _sempre debe ir despois_ de todos os cacth
+ Non se pode definir un finally se non existe, _polo menos_, un bloque try-catch
```java
public static void main(String[] args) {
    try {
        Empresa empresa = new Empresa("MiEmpresa");
        Empleado empleadoB1 = new Empleado("EmpleadoB1");
        Empleado empleadoD1 = new Empleado("EmpleadoD1");
        Empleado empleadoP = new Empleado("EmpleadoP1");

        empresa.getEmpleados().add(empleadoB1);
        empresa.getEmpleados().add(empleadoD1);
        empresa.getEmpleados().add(empleadoP);

        for (Empleado empdo : empresa.getEmpleados()) {
            empdo.setSueldo(empdo.calcularSueldo() / 1.05f);
        }
    } catch(SueldoMinimo | SueldoMaximo sm){
		System.out.println("Error -> " + sm.getMessage());
	} finally {
		System.out.println("Empleados con sueldo");
		for(Empleado empleado : empleadosConSueldo)
			System.out.println(empleado.getNombre());
	}
}    
```

## Resumo final
Se unimos todos os mecanismos de xestión de excepcións:
![[Pasted image 20250104124600.png]]
O obxeto `error` de `setSueldo` e o obxeto `sm` do bloque catch son o mesmo obxeto.

Un método A que invoca un método B que lanza unha excepción **non ten por qué realizar a captura da excepción**, senon que o método A pode delegar o tratmento da excepción a outro método C.
![[Pasted image 20250104125106.png | center | 600]]

Un programa que empregue este encadenamento de funcións quedaría da seguinte forma:
![[Pasted image 20250104125255.png]]