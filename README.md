# rxsqlite

RXSQLITE brings SQLITE functions to be used in your z/OS Rexx code. It is not a host command processor. It is an utility like EXECIO. You'll be able to issue DDL or DML statements.

This is only a routine to access SQLite API. The original sqlite shell is available in www.cbttape.org (https://www.cbttape.org/ftp/cbt/CBT965.zip)

The code was written in Enterprise COBOL using C API from CBT965 file.

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
