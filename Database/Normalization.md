# Explanation
- There is two way to design a database:
	1. ERD
		- We use it when we want to build the system form scratch or add a huge features to system.
	2. Normalization
		- We use it when we have a system already in use that has data but is having some issues.
- When we can say that database has issues?
	1. When there is duplicate data.
	2. Unexpected behavior of DML query.
	3. Slow system.
- **Normalization:** The process of structuring data to minimize duplication and inconsistencies.
- Normalization is the restructuring of tables to reach a healthy database.
- We can apply the normalization rules after creating ERD to verify its validity.
- The process usually involves breaking down a single Table into two or more tables and defining relationships between those tables.
## Goals:
***Goals is to avoid anomalies:***
- **Insertion Anomaly:** adding new rows forces user to create duplicate data.
- **Deleting Anomaly:** deleting rows may cause a loss if data that would be needed for other future rows.
- **Modification Anomaly:** changing data in a row forces changes to other rows because of duplication.

## Functional dependency:
- A constraint between two attributes (columns) or two sets of columns.
- A -> B if "For every valid instance of A, that value of A uniquely determines the value of B".
- Or ...A -> B if "Existing of B depending on a value of A".
- **Some Examples:**
	- Social security number determines employee name: SSN -> ENAME
	- Employee SSN and project number determines the hours per week that the employee works on the project {SSN, PNUMBER} -> HOURS
- **Types of functional dependency:**
	1. Full Functional Dependency:
		- Attribute is fully functional dependency on a PK if its value id determined by the whole PK.
	2. Partial Functional Dependency: 
		- Attribute if has a Partial Functional Dependency on a PK if its value is determined by part of the PK (Composite Key)
	3. Transitive Functional Dependency:
		- Attribute is Transitive Functional Dependency on a table if its value determined by anther non-key attribute which it self determined by PK.
	4. ![[functional_dependency.jpg]]
## Steps in Normalization:
1. **First Normal Form**:
	- Relation is in **first normal form** (1NF) if it contains no multivalued or composite attributes.
	- remove repeating groups to a new tables as already demonstrated, "carrying" the PK as a FK.
	- All columns (fields) must be atomic: Means no repeating items in columns.
2. **Second Normal Form:**
	- A relation is in **second normal form** (2NF) if it is in first normal form AND every non-key attribute is fully functionally dependent on the primary key.
	- i.e remove partial functional dependencies, so non-key attribute depends on just part of key.
3. **Third Normal Form:**
	- 2NF PLUS  no transitive dependencies (one attribute functionally determines a second, which functionally determines a third).
4. ![[norm_steps.jpg]]

# Sources
- [ITI Course: SQL Server -  Session 3](https://youtu.be/jZwvEgIwW_U?si=frkJKhx9rkQy08ap)