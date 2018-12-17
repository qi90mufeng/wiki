### isAssignableFrom() <-> instanceof <-> ==

> isAssignableFrom()方法是从类继承的角度去判断，instanceof关键字是从实例继承的角度去判断。
> isAssignableFrom()方法是判断是否为某个类的父类，instanceof关键字是判断是否某个类的子类。
> 使用方法：
>
> 父类.class.isAssignableFrom(子类.class)
>
> 子类实例 instanceof 父类类型
>
> isAssignableFrom()方法的调用者和参数都是Class对象，调用者为父类，参数为本身或者其子类。 
>
>
>
> Class<?> type
>
> type == HashSet.class

