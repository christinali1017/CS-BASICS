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



