# Using PMD

Pick a Java project from Github (see the [instructions](../sujet.md) for suggestions). Run PMD on its source code using any ruleset. Describe below an issue found by PMD that you think should be solved (true positive) and include below the changes you would add to the source code. Describe below an issue found by PMD that is not worth solving (false positive). Explain why you would not solve this issue.

## Answer

Pour le projet apache-commons-math dans le fichier /commons-math-legacy-core/src/test/java/org/apache/commons/math4/legacy/core/dfp/DfpTest.java à partir de la ligne 378
```java
if(op.equals("equal")){
    if(a.equals(b)!=result){
        assertionFailOpNum(op,num);
    }
}
```
PMD nous indique `CollapsibleIfStatements:	These nested if statements could be combined` ce qui semble en effet être un vrai positif on peut reécrire ce code de cette manière:

```java
if (op.equals("equal") && a.equals(b) != result)
{
    assertionFailOpNum(op, num);
}
```

Si jamais la seconde partie est dépendante de la première le code ne crachera pas car l'évaluation de l'opérateur && est paresseuse.

En ce qui concerne le fichier commons-math/commons-math-legacy-core/src/test/java/org/apache/commons/math4/legacy/core/jdkmath/AccurateMathTest.java à la ligne 1967
```java
x = 4503599627370497.0; // x = Math.pow(2, 52) + 1;
assertEquals("4503599627370497", new BigDecimal(x).toString());
```
l'erreur `AvoidDecimalLiteralsInBigDecimalConstructor:	Avoid creating BigDecimal with a decimal (float/double) literal. Use a String literal` est en faux positif car c'est de part la nature du test que cette erreur emerge il n'est ici pas question de bonne pratique.
