###Creating and Destroying Objects.
---


####Item 2: **Consider a builder when faced with many constructor parameters. --- Builder Pattern**

Example:

```java
public class User {
	private final String firstName; // required
	private final String lastName; // required
	private final int age; // optional
	private final String phone; // optional
	private final String address; // optional

	private User(UserBuilder builder) {
		this.firstName = builder.firstName;
		this.lastName = builder.lastName;
		this.age = builder.age;
		this.phone = builder.phone;
		this.address = builder.address;
	}

	public String getFirstName() {
		return firstName;
	}

	public String getLastName() {
		return lastName;
	}

	public int getAge() {
		return age;
	}

	public String getPhone() {
		return phone;
	}

	public String getAddress() {
		return address;
	}

	public static class UserBuilder {
		private final String firstName;
		private final String lastName;
		private int age;
		private String phone;
		private String address;

		public UserBuilder(String firstName, String lastName) {
			this.firstName = firstName;
			this.lastName = lastName;
		}

		public UserBuilder age(int age) {
			this.age = age;
			return this;
		}

		public UserBuilder phone(String phone) {
			this.phone = phone;
			return this;
		}

		public UserBuilder address(String address) {
			this.address = address;
			return this;
		}

		public User build() {
			return new User(this);
		}

	}
}

```

Example of create an above object:

```java
public User getUser() {
	return new
			User.UserBuilder('Jhon', 'Doe')
			.age(30)
			.phone('1234567')
			.address('Fake address 1234')
			.build();
}
```


####Item 3: Enforce the singleton property with a private constructor or an enum type

**A single-element enum type is the best way to implement a singleton**

singleton with static factory:

```java
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }
    public static Elvis getInstance() {
        return INSTANCE; 
    }
    public void leaveTheBuilding() { ... }
}
```

Enum singleton - the preferred approach

```java
public enum Elvis {
    INSTANCE;
    public void leaveTheBuilding() { ... }
}
```

####Item 5: Avoid creating unnecessary objects

Prefer primitives to boxed primitives, and watch out for unintentional auto-boxing.

####Item 6: Eliminate obsolete object references

Possible memory leaks:

- **Obsolete object reference**
- **cache**: If you’re lucky enough to implement a cache for which an entry is relevant exactly
so long as there are references to its key outside of the cache, represent the cache
as a WeakHashMap; entries will be removed automatically after they become obsolete.
Remember that WeakHashMap is useful only if the desired lifetime of cache
entries is determined by external references to the key, not the value.
- **listeners and callbacks**： If you implement an API where clients register callbacks but don’t deregister them explicitly, they will accumulate unless you take some action. The best way to
ensure that callbacks are garbage collected promptly is to store only weak references
to them, for instance, by storing them only as keys in a **WeakHashMap**.

**WeakHashMap**: Elements in a weak hashmap can be reclaimed by the garbage collector if there are no other strong references to the object, this makes them useful for caches/lookup storage.

Weak reference are not restricted to these hash tables, you can use WeakReference for single objects. They are useful to save resource, you can keep a reference to something but allow it to be collected when nothing else references it. (BTW, a string reference is a normal java reference). There are also weak references which tend not to be as readily collected as soft references (which don't tend to hang about for long after the last strong reference disappears)


###Methods Common to All Objects
---
This chapter tells you when and how to override the nonfinal Object methods.


All of its nonfinal methods (equals, hashCode, toString, clone, and finalize)
have explicit general contracts because they are designed to be overridden. **It is
the responsibility of any class overriding these methods to obey their general contracts**;
failure to do so will prevent other classes that depend on the contracts (such
as HashMap and HashSet) from functioning properly in conjunction with the class.

####Item 8: Obey the general contract when overriding equals
- **A superclass has already overridden equals, and the superclass behavior
is appropriate for this class**. For example, most Set implementations inherit
their equals implementation from AbstractSet, List implementations from
AbstractList, and Map implementations from AbstractMap.


- **So when is it appropriate to override Object.equals?** When a class has a
notion of logical equality that differs from mere object identity, and a superclass
has not already overridden equals to implement the desired behavior. This is generally
the case for value classes. A value class is simply a class that represents a
value, such as Integer or Date.

- **Rules** The equals method implements an equivalence relation. It is:
  * Reflexive: For any non-null reference value x, x.equals(x) must return true.
  * **Symmetric**: For any non-null reference values x and y, x.equals(y) must return
true if and only if y.equals(x) returns true.
  * **Transitive**: For any non-null reference values x, y, z, if x.equals(y) returns
true and y.equals(z) returns true, then x.equals(z) must return true.
  * Consistent: For any non-null reference values x and y, multiple invocations
of x.equals(y) consistently return true or consistently return false, provided
no information used in equals comparisons on the objects is modified.
  * For any non-null reference value x, x.equals(null) must return false.


####Item 9: Always override hashCode when you override equals

Failure to do so
will result in a violation of the general contract for Object.hashCode, which will
**prevent your class from functioning properly in conjunction with all hash-based
collections, including HashMap, HashSet, and Hashtable**.

####Item 10: Always override toString

- providing a good toString implementation makes your class
much more pleasant to use.
- When practical, the toString method should return all of the interesting
information contained in the object


####Item 11: Override clone judiciously

- If you override the clone method in a nonfinal class, you should
return an object obtained by invoking **super.clone.**
- Remember to copy internal data structure if needed.



