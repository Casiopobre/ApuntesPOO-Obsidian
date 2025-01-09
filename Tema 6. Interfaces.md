# Tema 6. Interfaces: abstracción e independencia de clases

## Concepto de interfaz
As **interfaces** establecen os requisitos que deben cumprir as clases do programa:
+ Defínense os _tipos de datos_ que se deben crear no programa
+ Defínense exactamente os _métodos_ que deben ter as clases do programa
+ Os _métodos de interés_ das clases son os indicados nas interfaces

Enténdense como un **compromiso ou acordo entre programadores**, de modo que a interfaz indica o que teñen que facer as clases, pero non como se ten que chegar a ese resultado, polo que outorga _liberdade_ e _abstracción_.

**Obxectivo**: establecer os _métodos visibles e accesibles_ polo resto do programa (en vermello na imaxe; do m10-m13) que unha clase debe implementar.
![[Pasted image 20250101233230.png | center | 250]]

O emprego de interfaces facilita o **desenvolvemeno e mantemento dos programas** xa que axudan á _división de responsabilidades_ entre os programadores e permiten unha _implementación independente_ das clases:
+ Cambiar unha _clase_ na que se implementan os métodos indicados na interfaz _non afectará ás outras clases_ que fan uso da devandita interfaz.
+ Un cambio na _interfaz_ sí que _afectará de forma significativa_ tanto ás clases que implementan a interfaz como ás que a empergan, polo que as interfaces ==unha vez se definen, non se deberían modificar==.

Una interfaz enténdese como unha **plantilla dunha clase**:
+ _Non teñen constructores_, xa que non se poden instanciar
+ As _clases deben implementar os métodos da interfaz_ para que esta poida ser empregada noutras clases: `public class <nome_clase>` **`implements`** `<nome_interfaz>`
+ Unha vez a interfaz é implementada, _compórtase como unha clase_.
![[Pasted image 20250102112722.png | center]]

A clase que implementa a interfaz pódese entender como unha **clase derivada da interfaz**, xa que _unha interfaz é equivalente a una clase abstracta_ con todos os métodos abstractos, todos os atributos constantes e sen constructores; polo que se poden _aplicar_ todos os conceptos de _herdanza, xerarquías, clases abstractas e poliformismo_.

> [!Exemplo]
> Na clase `Empresa` non se emprega a clase `EmpleadoImpl` senón que se emprega a intrfaz `Empleado`, polo que se podería cambiar a clase que implementa a interfaz sen ter que cambiar a clase empresa. Por exemplo, o método `getProyecto` ten a implementación realizada na clase `EmpleadoImpl`, polo que podemos cambiala sen modificar `Empresa`.

```java
public class Empresa {
    private ArrayList<Empleado> empleados;

    public ArrayList<Empleado> getEmpleados() {
        return empleados;
    }

    public void setEmpleados(ArrayList<Empleado> empleados) {
        this.empleados = empleados;
    }

    public ArrayList<Empleado> empleadosEnProyecto(String proyecto) {
        ArrayList<Empleado> empleadosEnProyecto = new ArrayList<>();
        for (Empleado empleado : empleadosEnProyecto)
            if (empleado.getProyecto(proyecto) != null) // <-----------
                empleadosEnProyecto.add(empleado);
        return empleadosEnProyecto;
    }
}
```

### Diferencias entre as clases abstractas e as interfaces
![[Pasted image 20250102113339.png | center]]

## Métodos por defecto
**Principal problema das interfaces**: as clases que as implementan non se poden _adaptar aos cambios_ que ocorren nas interfaces (engadir novos métodos abstractos, actualizar métodos... provoca _erros de compilación_ nas clases que implementan a devandita interfaz).
+ **Solución:** _métodos por defecto_

Os **métodos por defecto** son os que se deben _declarar e implementar na interfaz_ e que se _herdarán_ polas clases que a implementen:
```java
default public <tipo> <nome_metodo> (args *){ }
```
+ A implementación só debe empregar os args do método, xa que os atributos da interfaz son todos constantes
+ Os métodos por defecto poden ser sobrescritos nas clases que implementan a interfaz ou nas derivadas destas.

> [!Exemplo]
> No método `getProyectos` recíbese como arg a lista de proxectos nas que participou un empregado (que é un dos atributos da clase `Empleado`). Como non se pode acceder aos atributos de `Empleado`, ese atributo ten que pasarse como arg ao método por defecto.
```java
public interface Empleado {
    // Constantes
    float SUELDO_MAXIMO = 800000f;
    int MAXIMO_EMPLEADOS = 50;

    // Métodos abstractos
    float calcularSueldo();
    Proyecto getProyecto(String proyecto);
    ArrayList<Proyecto> getProyectos(float minimo);

    // Método por defecto
    default ArrayList<Proyecto> getProyectos(ArrayList<Proyecto> proyectos, String tipo) {
        ArrayList<Proyecto> proyectosTipo = new ArrayList<>();
        for (Proyecto proyecto : proyectos) {
            if (proyecto.getTipo().equals(tipo))
                proyectosTipo.add(proyecto);
        }
        return proyectosTipo;
    }
}
```

Os métodos por defecto son **implícitamente públicos**, e poden _chamar aos métodos abstractos da interfaz_ (que se implementarán nas clases que implementan a interfaz).

É importante valorar que tan convinte é definir métodos abstractos, especialmente se precisan args asociados a atributos das clases que implementan esas interfaces, xa que o código se volve máis complexo de entenedr e de manter.

Os métodos por defecto **herdanse** ás clases que implementan a interfaz, polo que tamén poden ser _sobrescritos_, empregando ou non `super`: `<nome_interfaz>.super.<metodo>`

## Métodos estáticos
Son os métodos que **poden ser invocados dende o inicio do programa**, polo que se poden _invocar sen instanciar_ a clase na que se definiron.
+ Pódense definir en _calquera clase_ ou en calquera _interfaz_.
+ Cárganse _automáticamente en memoria_ ao iniciar o programa
+ Só poden _invocar métodos estáticos_, xa que teñen que estar dispoñibles dente o arranque do programa.
+ _Non son herdados_.

> [!Exemplo]
> O método `beneficios` é un método estático, polo que se pode invocar en calquera momemento da forma `Empleado.beneficios(...)`.
```java
// DENTRO DA CLASE Empleado:
public static float beneficios(ArrayList<Float> presupuestos) {
    float beneficios = 0f;
    for(Float presupuesto : presupuestos)
        beneficios+=(presupuesto<100000)? 0.001*presupuesto:0.0001* presupuesto;
    return beneficios;
}
```

## Diferenzas entre os métodos estáticos e os por defecto
![[Pasted image 20250102141530.png | center]]

## Herdanza e interfaces
Pódese entender que **existe herdanza múltiple**, xa que unha clase que implementa unha interfaz é como unha clase derivada e, ademáis, unha clase pode implementar máis dunha interfaz.

Unha clase debe **implementar todos os métodos abstractos** das interfaces que implementa e **herda todos os métodos por defecto** de todas estas:
+ Se varias interfaces teñen en común algún _método abstracto_, a implementación dese método na clase será _válida_ para todos os interfaces
+ Se varias interfaces teñen en común algún _método estático_, non haberá _ningún conflicto_ (estes métodos non se herdan)
+ Se varias interfaces teñen en común algún _método por defecto_, existirá unha _colisión_ entre ambos métodos.

>[!No caso de que varias interfaces teñan en común algún método por defecto, cómo se resolve a herdanza deses métodos?]
> A clase que implementa as interfaces debe _sobrescribir_ os métodos por defectos que sexan comunes ás interfaces: pódese seleccionar a implementación empregando o **`super`**.
```java
public class EmpleadoImpl implements Empleado, EmpleadoBase {
    @Override
    public float beneficios(ArrayList<Float> presupuestos) {
        return EmpleadoBase.super.beneficios(presupuestos);
    }
}
```

Pódense crear **xerarquías de interfaces** igual que coas xerarquias de clases:
+ Existe _herdanza múltiple_ entre interfaces
+ As interfaces derivadas _herdarán_ todos os métodos da interfaz base (_excepto os estáticos_)
+ Pódense _sobrescribir os métodos por defecto_
+ _Unha clase non pode extender unha interfaz nin viceversa_
![[Pasted image 20250102145026.png | center | 550]]
As xerarquías combinan a herdanza de clases e de interfaces e a implementación de interfaces por parte de clases, polo que poden resultar _moi complexas_, pero é importante que _se manteñan facilmente extensibles_.
