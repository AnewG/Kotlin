```

public abstract class Pizza {
    
    public enum Topping {
        HAM,
        MUSHROOM,
        ONION,
        PEPPER,
        SAUSAGE
    }
    final Set < Topping > toppings; // Topping类型的Set->toppings

    //T类型只能是Builder或它的派生类，因为Builder本身是个泛型类，在描述「某个具体的Builder类型」时，就必须带上类型参数。对于这里来说就是T。T extends Builder 严格来说是错误的。
    //当然，对于 Java 来讲，你不带 T 也是完全没问题的，编译器也不会给你警告，最多让 IDEA 提示一句「Raw use of parameterized class」，毕竟 Java 的泛型编译后都会被擦除，运行是时候都是一样的。不过，带上泛型更有利于编译器检查，也更有利于写出类型安全的代码。
    abstract static class Builder < T extends Builder < T >> {  
        
        EnumSet < Topping > toppings = EnumSet.noneOf(Topping.class);
        
        public T addTopping(Topping topping) {
            toppings.add(Objects.requireNonNull(topping));
            return self();
        }
        
        abstract Pizza build();

        // Subclasses must override this method to return "this" 
        /*
        一般来说，把父类型的对象转换为子类型的对象，都要用强制类型转换
          interface Base {}
          class Derived extends Base {}
          Base obj = new Derived();
          Derived derivedObj = (Derived) obj;
        这样做很不优雅，也不「type safe」。不过利用递归的类型参数，可以避免强制类型转换
          interface Base<T extends Base<T>> {
              T self();
          }
          class Derived extends Base<Derived> {
              @Override
              Derived self() {
                  return this;
              }
          }
          Base<Derived> obj = new Derived();
          Derived other = obj.self(); //父类型对象.self()=子类型对象
        */
        protected abstract T self();
    }

    //Pizza构造器，参数是Builder类型的builder，<?> is a shorthand for <? extends Object>
    //因为 Builder 声明为 T extends Builder<T> 就保证了 T 一定是 Builder 的子类型， 这里就没有必要再重复限制一次了。
    Pizza(Builder < ? > builder) {
        toppings = builder.toppings.clone();
    }
}

public class NyPizza extends Pizza {
    
    public enum Size {
        SMALL,
        MEDIUM,
        LARGE
    }
    private final Size size;
    
    // < Builder > 里的 Builder 是 NyPizza.Builder，这里限制了类型，避免 Calzone.Builder 传入也能正常运行。类型安全检查在编译期间就完成了
    public static class Builder extends Pizza.Builder < Builder > { 
        private final Size size;
        public Builder(Size size) {
            this.size = Objects.requireNonNull(size);
        }
        @Override public NyPizza build() {
            return new NyPizza(this);
        }
        @Override protected Builder self() {
            return this;
        }
    }

    private NyPizza(Builder builder) {
        super(builder);
        size = builder.size;
    }
}
public class Calzone extends Pizza {
    
    private final boolean sauceInside;
    
    public static class Builder extends Pizza.Builder < Builder > {
        private boolean sauceInside = false; // Default 
        public Builder sauceInside() {
            sauceInside = true;
            return this;
        }
        @Override public Calzone build() {
            return new Calzone(this);
        }
        @Override protected Builder self() {
            return this;
        }
    }

    private Calzone(Builder builder) {
        super(builder);
        sauceInside = builder.sauceInside;
    }
}


NyPizza pizza = new NyPizza.Builder(SMALL).addTopping(SAUSAGE).addTopping(ONION).build();
Calzone calzone = new Calzone.Builder().addTopping(HAM).sauceInside().build();

```
