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

- Obsolete object reference
- **cache**: If you’re lucky enough to implement a cache for which an entry is relevant exactly
so long as there are references to its key outside of the cache, represent the cache
as a WeakHashMap; entries will be removed automatically after they become obsolete.
Remember that WeakHashMap is useful only if the desired lifetime of cache
entries is determined by external references to the key, not the value.
- listeners and callbacks： If you implement an API where clients register callbacks but don’t deregister them
explicitly, they will accumulate unless you take some action. The best way to
ensure that callbacks are garbage collected promptly is to store only weak references
to them, for instance, by storing them only as keys in a WeakHashMap.





