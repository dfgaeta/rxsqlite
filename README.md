# rxsqlite

RXSQLITE brings SQLITE database functions to be used in your z/OS Rexx code. It is not a Rexx host command processor. It is an utility like EXECIO. You'll be able to issue DDL or DML statements. The tool is useful since we don't need to coding lot of SQLITE apis, who did or do this know about I mean...

This is only a routine to access SQLite API. The original sqlite3 shell is available in www.cbttape.org (https://www.cbttape.org/ftp/cbt/CBT965.zip)

The code was written in Enterprise COBOL using C API from CBT965 file.

The main SQLITE parameters are EXEC and QUERY followed by variable with SQL statement. To EXEC parameter two variables will be assigned, SQLCODE and SQLAFFCT. SQLCODE will not contain DB2 error codes, but SQLITE error codes. SQLAFFCT will be assigned with a total of updated/deleted/inserted records for execution.

In QUERY parameter, the result of SELECT will assign Rexx variables as a STEM structure. As default the returned variables has a "$" as a field prefix. Like EXEC parameter, some Rexx variables will be assinged. SQLCODE and SQLRECS, the last one has a total of records retrieved in a query.

Examples :

/* REXX */                         
                                   
  'SQLITE INIT'                    
  DBIO_DBNAME='/u/gaeta/dbs.db'    
  ESQL='CREATE TABLE tst1 (a text, b int,c text)'          
  'SQLITE EXEC ESQL /POSIX(ON)'    
  SAY 'sqlcode=' sqlcode

/* REXX */
SAY 'SELECT...'                                                
ESQL='SELECT cod,nome,salario from tab3 ORDER BY COD'          
                                                               
'SQLITE QUERY ESQL /POSIX(ON)'                                 
SAY 'SQLITE SQLRECS=' SQLRECS                                  
SAY 'SQLITE RC=' RC                                            
DO I=1 TO SQLRECS                                              
  SAY $cod.i $nome.i $salario.i format($salario.i/100,17,2)    
END                                                            
                                                               


Enjoy!
