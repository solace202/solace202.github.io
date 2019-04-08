### Java - static 执行顺序

Father类

```java
public class Father {
   public int a = a();

   public static int b = b();

   int a() {
      System.out.println("Father normal variable init... ...");
      return 1;
   }

   static int b() {
      System.out.println("Father static variable init... ...");
      return 1;
   }

   static {
      System.out.println("Father static... ...");
   }

   {
      System.out.println("Father normal... ...");
   }

   Father() {
      System.out.println("Father constructor... ...");
   }
}

```

Son类

```Java
public class Son extends Father{
   public int a = a();

   public static int b = b();

   int a() {
      System.out.println("Son normal variable init... ...");
      return 1;
   }

   static int b() {
      System.out.println("Son static variable init... ...");
      return 1;
   }

   static {
      System.out.println("Son static... ...");
   }

   {
      System.out.println("Son normal... ...");
   }

   Son() {
      System.out.println("Son constructor... ...");
   }

   public static void main(String[] args) {
      Son son = new Son();
   }
}
```

输出结果：

```Java
Father static variable init... ...
Father static... ...
Son static variable init... ...
Son static... ...

Son normal variable init... ...
Father normal... ...
Father constructor... ...

Son normal variable init... ...
Son normal... ...
Son constructor... ...
```

