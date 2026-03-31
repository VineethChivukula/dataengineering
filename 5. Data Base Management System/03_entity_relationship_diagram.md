# Entity-Relationship (ER) Diagram

An Entity-Relationship (ER) Diagram is a visual representation of the entities within a system and the relationships between those entities. It is commonly used in database design to illustrate the structure of a database and how different entities interact with each other.

## Components of an ER Diagram

There are few components in an ER Diagram, and we will discuss each of them in detail.

### Entities

An entity is a real-world object, concept or a thing about which the data can be stored. The tables in a database represent entities. For example, in a university database, entities could be "Student", "Course", "Book" etc.
An entity is represented by a rectangle in an ER diagram.

![Entity Representation](images/entity.png)

An Entity Set is a collection of similar types of entities. For example, all the students in a university can be considered as an entity set.

There are two types of entities:

1. **Strong Entity:** A strong entity is an entity that can exist independently of other entities. It has a primary key that uniquely identifies each instance of the entity. For example, a "Student" entity can be considered a strong entity because it can exist independently and has a unique identifier (e.g., student ID).

2. **Weak Entity:** A weak entity is an entity that cannot exist independently and relies on a strong entity for its existence. It does not have a primary key of its own and is identified by a combination of its attributes and the primary key of the strong entity it depends on. For example, a "Course Enrollment" entity can be considered a weak entity because it cannot exist without the "Student" entity and is identified by the combination of the student ID and course ID.

In order to differentiate between strong and weak entities in an ER diagram, we use different notations. A strong entity is represented by a rectangle with a single border, while a weak entity is represented by a rectangle with a double border.

![Entity Types Representation](images/entity_types.png)

### Attributes

Attributes are the properties or characteristics of an entity. They provide more information about the entity and help to describe it in more detail. For example, for a "Student" entity, attributes could include "Student ID", "Name", "Roll No", "Age", "Major" etc. An attribute is represented by an oval in an ER diagram.

![Attribute Representation](images/attribute.png)

There are four types of attributes:

1. **Simple Attribute:** A simple attribute is an attribute that cannot be further divided into smaller parts. For example, "Email" is a simple attribute because it cannot be broken down into smaller components.
2. **Composite Attribute:** A composite attribute is an attribute that can be divided into smaller sub-parts. For example, "Name" can be considered a composite attribute because it can be broken down into "First Name" and "Last Name".
3. **Derived Attribute:** A derived attribute is an attribute that can be derived from other attributes. For example, "Age" can be considered a derived attribute because it can be calculated from the "Date of Birth" attribute.
4. **Multivalued Attribute:** A multivalued attribute is an attribute that can have multiple values for a single entity. For example, "Phone Number" can be considered a multivalued attribute because a person can have multiple phone numbers.
5. **Key Attribute:** A key attribute is an attribute that uniquely identifies an entity within an entity set. For example, "Student ID" can be considered a key attribute because it uniquely identifies each student in the "Student" entity set.

In order to differentiate between simple, composite, derived, and multivalued attributes in an ER diagram, we use different notations. A simple attribute is represented by a single oval, a composite attribute is represented by an oval with sub-ovals, a derived attribute is represented by a dashed oval, and a multivalued attribute is represented by a double oval, while a key attribute is represented by an oval with an underline.

![Attribute Types Representation](images/attribute_types.png)

### Relationships
