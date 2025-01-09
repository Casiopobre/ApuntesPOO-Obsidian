# Tema 5. Poliformismo: herdanza e simplificación de código
## Poliformismo en herdanza
É o mecanismo mediante o cal un obxeto se pode _comportar de múltiples formas_ en función do _contexto_ do programa: pódese comportar como unha _instancia da clase á que pertence_ (new) ou como unha _instancia dalgunha das clases superiores_. 

O poliformismo está **relacionado coa herdanza** e co uso das clases que se herdan:
![[Pasted image 20241230184110.png | center | 600]]
```java
1 InfateriaEuropa infEuropa = new InfanteriaEuropa("AMARELO");
2 Infanteria infan = infEuropa;
3 CartaDeEquipamiento cartaEquip = infEuropa;
```
Liña 1: Crease un obxeto da clase `InfanteriaEuropa` (`infEuropa`)
Liña 2: Fórzase a `infEuropa` a actuar como un obxeto da súa clase base (`Infanteria`)
Liña 3: Fórzase a `infEuropa` a actuar como un obxeto da clase _abstracta_ superior.

> [!Como pode un obxeto comportarse como unha clase abstracta?]
Realmente a única restricción que teñen neste aspecto as clases abstractas, e que non se poden instanciar, polo que non se pode empregar `new` para invocar aos seus constructores, pero sí que se poden empregar, ademáis de para estructurar as xerarquías de clases, para _restrinxir os métodos que poden invocar os obxetos_.

## Upcasting e Downcasting
Ocorre cando se quere que un _obxeto se comporte como unha clase á que non pertence_, xa que se lle está forzando un **cambio no tipo de dato** do obxeto:
+ **Upcasting**: cando un obxeto dunha clase derivada se comporta como un da clase base (de abaixo arriba)
+ **Downcasting**: cando un obxeto da clase base se comporta como un das clases derivadas (de arriba abaixo)
![[Pasted image 20241230185543.png | center | 600]]

Esto _non implica unha nova reserva de memoria_, xa que o obxeto seguirá sendo o mesmo, aínda que o casting tamén conleva un _cambio na accesibilidade_ dos atributos e dos métodos que se poden invocar dende o obxeto.

### Upcasting
É o máis habitual, xa que parece o máis natural. Cando se realiza un upcasting, _non é necesario indicar de forma explícita un **cast**_  e _se perde a **accesibilidade** aos métodos e atributos propios_, xa que o obxeto deixa de comportarse como esa clase.

Se un **método está sobreescrito**, cando se fai o upcasting, o obxeto empregará a implementación correspondente á _clase á que pertence o obxeto_, xa que se empregase as implementacións da outra clase, non existiría poliformismo no caso das clases abstractas.

O upcasting é un **concepto clave** na POO, xa que, _se é necesario o seu uso no programa, entón deberase aplicar o mecanismo de herdanza_, o que _simplifica_ o deseño do programa.

Empregando upcasting, **nunca se producirá un erro** xa que a _herdanza_ garante que as clases derivadas teñan os mesmos métodos que a clase base.
**==!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!==** **[[Preguntas tipo exame POO#Pregunta 4. Tema 5 Upcasting| PREGUNTA DE EXAME!!!]]** **==!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

### Downcasting
Co downcasting **fórzase** ao obxeto da clase base a comportarse como un da clase derivada, polo que non se pode asegurar que esto se cumpla, o que fai que sexa unha opción _unsafe_ que pode xerar un erro (_ClassCastException_). Así, típicamente _emprégase para desfacer un upcasting_.

**==!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!==** **[[Preguntas tipo exame POO#Pregunta 5. Tema 5 Downcasting| PREGUNTA DE EXAME!!!]]** **==!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

É **necesario castear** o obxeto á clase na que se convertirá: 
`Infanteria inf = (Infanteria) carta`

> [!Principal problema]
_Non se pode garantir que se poida realizar correctamente o downcasting_, xa que ten lugar en _tempo de execución_ (só se comproba que o obxeto sexa dunha clase derivada (**`instanceof`**)). Ademáis, aínda que o obxeto soporte os mesmos atributos e métodos, se o tipo de obxeto non é unha clase derivada, xerarase unha excepción.

O operador **`instanceof`** determina en tempo de execución se o tipo de dato dun obxeto é unha clase dada: `<nome_obxeto> instanceof <nome_paquete>.<nome_clase>`
[[Exemplos MonoPOOly#Exemplo 1 instanceof|Exemplo do emprego de instanceof no Monopoly]]

## Benficios do poliformismo
+ Facilita a simplificación do código do programa
+ Facilita a extensibilidade dos progrmas

