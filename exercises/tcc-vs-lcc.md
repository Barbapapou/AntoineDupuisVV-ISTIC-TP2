# TCC *vs* LCC

Explain under which circumstances *Tight Class Cohesion* (TCC) and *Loose Class Cohesion* (LCC) metrics produce the same value for a given Java class. Build an example of such as class and include the code below or find one example in an open-source project from Github and include the link to the class below. Could LCC be lower than TCC for any given class? Explain.

## Answer

TCC ET LCC ont la même valeur lorsque toutes les méthodes de la classe sont directement connectées et qu'il n'y a pas de connexions indirectes entre les méthodes. 

```java
public class ExampleClass 
{
    public void methodA() 
    {
        // code
    }

    public void methodB() 
    {
        // code
    }

    public void methodC() 
    {
        // code
    }
}
```

Le LCC peut être inférieur au TCC pour une classe donnée. Cela se produit lorsqu'il existe des connexions indirectes entre des méthodes qui ne sont pas étroitement liées.

```java
public class ExampleClass 
{
    public void methodA() 
    {
        // code
        methodB();
    }

    public void methodB() 
    {
        // code
    }

    public void methodC() 
    {
        // code
        methodB();
    }
}
```