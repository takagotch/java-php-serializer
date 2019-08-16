### java-php-serializer
---
https://github.com/marcospassos/java-php-serializer

```java
Serializer serializer = new SerializerBuilder()
  .addExclusionStrategy(new MyCustomExclusionStrategy())
  .setNamingStrategy(new MyCustomNamingStrategy())
  .registerBuiltinAdapters()
  .setCharset(Charset.forName("ISO-8859-1"))
  .registerAdapter(CustomObject.class, new CustomObjectAdapter())
  .build();
  

List list = new ArrayList();
list.add("A string");
list.add(12345);
list.add(true);
System.out.println(serializer.serialize(list));

public class UnderscoreNamingStrategy implements NamingStrategy
{
  public String getClassName(Class type)
  {
    return type.getName();
  }
  
  public String getFieldName(Field field)
  {
    if (Modifier.isPrivate(field.getModifiers())) {
      return "_" + field.getName();
    }
    
    return field.getName();
  }
}

public class EnumTypeAdapter implements TypeAdapter<Enum>
{
  public void write(Enum value, Writer writer, Context context)
  {
    writer.writeString(value.name());
  }
}

public class MyCustomAdapter implements TypeAdapter<CustomObject>
{
  @Override
  public void write(CustomObject object, Writer writer, Context context)
  {
    int reference = context.getReference(object);
    
    if (reference > 0) {
      writer.writeObjectReference(reference);
      
      return;
    }
    
    context.setReference(reference, object);
  }
}


```

```
```

```
```
