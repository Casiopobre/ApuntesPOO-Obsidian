## Exemplo #1: instanceof
Arquivo: monopoly.casillas.Solar.java (ln 18-26)
```java
public int getNumeroCasas(){
	int counter = 0;
	for (Edificio i : edificios){
		if (i instanceof Casa){
		counter++;
		}
	}
	return counter;
}
```
Comproba cantos edificios do tipo `Casa` hai no solar recorrendo o ArrayList de `edificios`.
