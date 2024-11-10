ERD classword 8

Entities - This ERD consist of a supertype entity and several subtype employees:

Supertype:
    Employee entity:
        EmployeeID UNSIGNED INT PK 
        Fname VARCHAR
        Lname VARCHAR
        DOB DATE
        Address VARCHAR 
        SSN INT VARCHAR

        employee_type VARCHAR
        is_manager BOOLEAN
        compensation_type VARCHAR NOT NULL


Subtypes:
    {
        DISJOINT CONSTRAINT: An employee can be only one of the three. ex: They cannot be both a engineer and technician.
        PARTIAL CONSTRAINT: An employee may or may NOT be one of its subtypes.


        Secretary entity:
            EmployeeID UNSIGNED INT PK FK 
            TypingSpeed SMALLINT

        Technician entity:
            EmployeeID UNSIGNED INT PK FK 
            Tgrade SMALLINT

        Engineer entity:
            EmployeeID UNSIGNED INT PK FK 
            EngType VARCHAR

    },
    {
        DISJOINT CONSTRAINT: This constraint is not necessary because there is one option, but it can only be one of its subtypes.
        PARTIAL CONSTRAINT: An employee does NOT need to be a manager.


        Manager:
            EmployeeID UNSIGNED INT PK FK 
            MgrDeptCode UNSIGNED INT
            Manages several(Project entity)

    },
    {
        DISJOINT CONSTRAINT: An employee is either salaried or hourly but not both.
        COMPLETE CONSTRAINT: An employee MUST be either a salaried or hourly employee.

        Salaried_Employee:
            EmployeeID UNSIGNED INT PK FK 
            salary UNSIGNED INT

        Hourly_Employee:
            EmployeeID UNSIGNED INT PK FK 
            PayScale FLOAT
            belongs to ONE(TradeUnion entity)
    }

other entites:
    Project:
        Prj_id  UNSIGNED INT PK_CONSTRAINT
        Prj_desc VARCHAR
        Mgr_dept_code UNSIGNED INT FK_CONSTRAINT

    TradeUnion:
        TUnion_Id UNSIGNED INT PK_CONSTRAINT
        City VARCHAR

relationships:
    Employee - IS A -  {Secretary, Technician, Engineer}, {Manager}, {Salaried_Employee, Hourly_Employee}

    Manager - MANAGES - Projects
    One to Many relationship: because one manager can manage several projects & one project can only have a single manager

    Hourly_Employee - BELONGS TO - TradeUnion
    Many to one relationship: because an hourly employee belongs to one and only one trade union. a trade union can have many employees.

