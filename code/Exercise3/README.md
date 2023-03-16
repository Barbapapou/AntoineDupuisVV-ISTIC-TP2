# Code of your exercise

Put here all the code created for this exercise
```xml
<rule name="DetectDeeplyNestedIf" language="java">
    <xpath>
        //IfStatement[count(ancestor::IfStatement) &gt;= 3]
    </xpath>
</rule>
```
