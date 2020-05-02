
# Effective Java Notes

## Consider static factory method instead of public constructor

### Advantage
* One advantage of static factory methods is that, unlike constructors, they have names.
* A second advantage of static methods is that, unlike constructors, they are not required to create a new object each time they're invoked.
* A third advantage of static factory methods is that, unlike constructors, they can return an object of any subtype of their return type. This gives you great flexibility in choosing the class of the reurned object.
* A fourth advantage of static factories is that the class of the returned object can vary from call to call as a function of the input parameters.
* A fifth advantage of static factories is that the class of the returned object nedd not exists when the class containing the method is written.

### Disadvantage

* The main limitation of providing only static factory methods is that classes without public or protected constructors cannot be subclassed.
* A second shortcoming of static factory methods is that they are hart for programmers to find.

## 2. Consider a builder when faced with many constructor parameters.

## 3. Enforce the singleton property with a private constructor or an enum type.

## 4. Perfer try-with-resources to try-finally(Since Java7).

## 5. Override equals

>* Use the == operater to check if the argument is a reference to this object;
>* Usb the instanceof operator to check if the argument has the correcttype;
>* Cast the argument to the correct type;
>* For each \significant\ field in the class, check if that field of theargument matches the corresponding field of this object.

## 6. Override clone judiciously

In practise, a class implementing Clonable is expected to provide a properly functioning public clone method.

## 7. In Java 8, the Comparator interface was outfited with a comparator construction methods, which enable fluent construction of comparators.

    ```java
    private static Comparator<PhoneNumber> comparator = 
            Comparator.comparingInt((PhoneNumber pn) -> pn.areaCode).
            thenComparingInt(pn -> pn.prefix).
            thenComparingInt(pn -> pn.lineNum);

    @Override,
    public int compareTo(@NotNull PhoneNumber o) {
        return comparator.compare(this, o);
    }
    ```

In summary, whenever you implement a value class that has a sensible ordering, you should have the class implement the Comparable interface so that the instance can be easily sorted, searched, and used in comparison-based collections. avoid the use of the **< and >**  operators. Instead, use the static compare methods in the boxed primitive classes or the comparator construction methods in the Comparator interface.

## 8. Note that a nonzero-length array is always mutable, so it is wrong for a class to have a public static final array field, or an accessor that returns such a field.
