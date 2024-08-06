# Explanation

## DB Life Cycles:
1. Analysis -> System Analyst (Requirement, Doc)
2. DB Design -> DB Designer (ERD)
3. DB Mapping -> DB Designer (Set of Rules, Actual Schema, Table)
4. DB Implementation -> DB Developer (Physical DB, Tool, RDBMS {SQL Server, MySql, Oracle, ..}) 
5. Application (GUI) -> Application Programmer (DB User)
6. Client -> End User -> Browser -> URL

## File Based System
### Disadvantages and Limitations
1. Difficult search.
2. Low performance.
3. Separated copies.
4. No relationship.
5. No DB integrity.
6. DB duplication.
7. Long development time.
8. Security & Performance.
9. Constraints & Rules.
10. No data quality.
11. Manual backup & restore.
12. No standard.
13. Difficult integration.

## DBMS System
### Advantages
- Standardization and better data accessibility and response (SQL).
- **Sharing Data:** different users get different views of data.
- Enforcing integrity constrains.
- **Improved Data Quality:** constraints, data validation rules.
- Inconsistency can be avoided because of data sharing.
- Restricting unauthorized access.
- **Providing Backup and Restore:** disaster recovery is easier.
- **Minimal Data Redundancy:** leads to increased data integrity/consistency.
- **Program-Data Independence:** 
	- Metadata stored in DBMS, so application don't worry about data formats.
	- Data queries/updates managed by DBMS.
### Disadvantages
1. Its need expertise to use.
2. DBMS itself is expensive.
3. The DBMS may be incompatible with any other available DBMS.
### Database System
- ![[database_system.png]]
# Sources
- [Session 1 - ITI Course: Database, SQL Server](https://youtu.be/9dW34UI520Y?si=PZaxLqVGidnGIcnn)