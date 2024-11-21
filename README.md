# Pluggable-Database-manipulation
====================================================
Pluggable database creation, deletion and EOM (Oracle Enterprise Management)
===============================================================

This repository provides essential SQL scripts and guidelines for managing Pluggable Databases (PDBs) in Oracle's Multitenant architecture. 
The scripts cover the creation, deletion, and general management of PDBs, along with insights into Oracle Enterprise Management tools.

Scripts Overview
===================

TASK1
========

: Creation of pluggable database:

Query: CREATE PLUGGABLE DATABASE plsql_class2024db
  ADMIN USER he_plsqlauca IDENTIFIED BY herve123
  FILE_NAME_CONVERT = ('E/ORACLE/ORADATA/ORCL21\pdbseed', 'E:/ORACLE/ORADATA/ORCL21\PLSQL_class2024db');

  Purpose: This query creates a new PDB named plsql_class2024db.
  ***The new PDB will initially be a clone of the pdbseed database, which serves as a template for creating PDBs.
  ADMIN USER he_plsqlauca IDENTIFIED BY herve123
Purpose: Specifies the administrative user for the new PDB.

ADMIN USER he_plsqlauca IDENTIFIED BY herve123
========================================
# he_plsqlauca: The username of the admin user for this PDB.
# herve123: The password for the admin user.
This user will have sufficient privileges to manage the new PDB (like a SYS user for this PDB).

FILE_NAME_CONVERT
====================
# Source Path: E/ORACLE/ORADATA/ORCL21\pdbseed
This is the location of the template datafiles (from the pdbseed PDB).

# Target Path: E:/ORACLE/ORADATA/ORCL21\PLSQL_class2024db
This is where the datafiles for the new PDB will be stored.
Oracle will copy the datafiles from the source directory (pdbseed) to the specified target directory (PLSQL_class2024db).


TASK 2: 
========

DELETION OF A NEW PLUGGABLE DATABASE
=====================================
1.CREATION OF THE 2ND DELETABLE PDB FIRST
=============================

Query: CREATE PLUGGABLE DATABASE HE_TO_DELETE_PDB
ADMIN USER he_plsqlauca IDENTIFIED BY herve123
FILE_NAME_CONVERT = ('E:\ORACLE\ORADATA\ORCL21', 'E:\ORACLE\ORADATA\ORCL21\he_to_delete_pdb');

2. CLOSE THE PLUGGABLE DATABASE
   ==============================

  Query: ALTER PLUGGABLE DATABASE HE_TO_DELETE_PDB CLOSE IMMEDIATE;
  
  Command Purpose: Unplugs the PDB HE_TO_DELETE_PDB, preparing it for deletion or relocation

4. Drop the Unplugged Pluggable Database
   ================================

   Query: DROP PLUGGABLE DATABASE HE_TO_DELETE_PDB INCLUDING DATAFILES;
   
   Command Purpose: Successfully drops the unplugged PDB HE_TO_DELETE_PDB, along with its associated datafiles.

TASK 3: 
===============

ORACLE ENTERPRISE MANAGEMENT
=================================
This section demonstrates the Oracle enterprise management dashboard (EOM)

To login the EOM, you use the URL: https://localhost:8088/em
Then it will demonstrate the EOM login page with 3 fields: 

USERNAME, PASSWORD and CONTAINER NAME, then we use USERNAME AS "SYS", PASSWORD, and then login.
