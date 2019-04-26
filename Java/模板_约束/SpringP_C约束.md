# P

p: property		属性

c: construction	构造

spring配置文件中，通过P来简写

```xml
<-- 传统 -->
<bean id="..." class="">
    <constructor-arg index="0" ref="xxx" />
    <constructor-arg index="3" value="xxx" />
    <property name="name" value/ref="zhangsan" ></property>
</bean>
<-- p/c -->
<bean id="..." class="..." p:name-ref="zhangsan" p:name="zhangsan" c:_0-ref="xxx" c:_3="xxx" >
    
</bean>
    
```











