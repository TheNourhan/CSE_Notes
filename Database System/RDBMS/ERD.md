# Explanation
- Entity Relationship Diagram (ERD)
- identifies information required by business by displaying the relevant entities and the relationships between them.

## The ER Model
Basic constructs of the E-R model:
1. **Entities:** person, place, object, event, concept (often corresponds to a real time object that is distinguishable from any other object). **Rectangles**
2. **Attributes:** property or characteristic of any entity type (often corresponds to a field in a table). **Ellipses**
3. **Relationship:** link between entities (corresponds to primary key-foreign key equivalencies in related tables). **Diamonds**
4. ![[ER_diagrams.png]]

## Strong Entities Vs Weak Entities
- **Strong Entities:** an entity set that a primary key.
- **Weak Entities:** an entity set that do not have sufficient attributes to form a primary key.

- **Partial Key:** a set of attributes that can be associated with PK of an owner entity set to distinguish a weak entity.
- If the parent disappears, the child must disappear too.
- For example: If you delete the account, the transaction must be deleted.
- ![[weak_entity.png]]

## Types of Attributes
1. **Simple Attribute:** If it is indivisible, not calculated at run time (It does not need an equation to calculate it), and not repeated for the same entity.
	- ![[simple_attribute.png]]
2. **Composite Attribute:** If it is divided (Name: first + last).
	- ![[composite_attribute.png]]
3. **Multi-Valued Attribute:** Something that is repeated for the same entity (Phone, Address, ..).
	- ![[multi-valued_attribute.png]]
4. **Derived Attribute:** If it can be calculated at runtime (equation: Age = current year - birth year).
	- ![[derived_attribute.png]]
5. **Complex Attribute:** Multi-Valued + Composite.
	- ![[complex_attribute.png]]

## Relationship
- A relationship is an association among several entities.
- A relationship may also have attributes.
- For example: consider the entity sets customer and loan the relationship set borrower. We could associate the attribute **data-issued** to the relationship to specify the data when the loan was issued.
### Properties
Relation has three properties:
1. **Degree of Relationship:** number of entity types that participate in a relationship.
	- **Unary:** between two instances of one entity type. 
		- **Recursive Relationships:** a relationship in which the same entity participates more than once.
	- **Binary:** between the instances of two entity type. 
	- **Ternary:** among the instances of three entity type. 
		- It is a rare condition where a trait exists among three or more entities.
	- ![[degree_of_relationship.png]]
2. **Cardinality Constraint:** how many instances of one entity will or must be connected to a single instance from the other entities.
	- **One-One Relationship**
	- **One-Many Relationship**
	- **Many-Many Relationship**
	- ![[cardinality_constraint.png]]
3. **Participation Constraint:** key words (may, zero or more, optional).
	- For example: A department may hire many employees.
	- ![[participation_constraint.png]]

## Keys
Different Types of keys:
- **Candidate Key:** is a set of of one or more attribute whose value can uniquely identify an entity in the entity set.
	- Any attribute in the candidate key cannot be omitted without destroying the uniqueness property of the candidate key.
	- Candidate key could have more than one attributes.
- **Primary Key:** is the candidate key that is chosen by the database designer as the unique identifies of an entity.
	- Primary key may be composite.
- Foreign Key
- Composite Key
- Partial Key
- Alternate Key
- Super Key

# Sources
- [Session 1 - ITI Course: Database, SQL Server](https://youtu.be/9dW34UI520Y?si=PZaxLqVGidnGIcnn)