# utl-eliminating-warning-when-macro-argument-refers-back-to-previous-argument
Eliminating warning when macro argument refers back to previous argument.
    Eliminating warning when macro argument refers back to previous argument                                                
                                                                                                                            
    IBM JCL allows this without a warning.                                                                                  
                                                                                                                            
    Two Solutions                                                                                                           
                                                                                                                            
       1. %nrstr solution ( you need to unquote)                                                                            
          "data _null_;" <datanull@GMAIL.COM                                                                                
                                                                                                                            
       2. Single quotes (reminds you that you have to unquote)                                                              
          Eye of the beholder. A little less Klingon?                                                                       
                                                                                                                            
                                                                                                                            
    github                                                                                                                  
    https://tinyurl.com/y9jsbd3e                                                                                            
    https://github.com/rogerjdeangelis/utl-eliminating-warning-when-macro-argument-refers-back-to-previous-argument         
                                                                                                                            
    SAS-L                                                                                                                   
    https://listserv.uga.edu/cgi-bin/wa?A2=SAS-L;274a3c9.1902a                                                              
                                                                                                                            
                                                                                                                            
    PROBLEM                                                                                                                 
    =======                                                                                                                 
                                                                                                                            
    %macro class (var1=,var2=,var3=);                                                                                       
                                                                                                                            
    proc print data = sashelp.class;                                                                                        
       var &var1. &var2.;                                                                                                   
       where &var3. ;                                                                                                       
    run;                                                                                                                    
                                                                                                                            
    %mend class;                                                                                                            
                                                                                                                            
    %class (var1=weight,var2=age,var3=&var2 ge 14 and sex = "M");                                                           
                                                                                                                            
                                                                                                                            
    *          _       _   _                                                                                                
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                                
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                                               
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                               
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                               
                                                                                                                            
    ;                                                                                                                       
                                                                                                                            
                                                                                                                            
    1. %nrstr solution ( you need to unquote)                                                                               
    ------------------------------------------                                                                              
                                                                                                                            
    %macro class (var1=,var2=,var3=);                                                                                       
                                                                                                                            
    %let var3=%str(%unquote(&var3));                                                                                        
                                                                                                                            
    proc print data = sashelp.class;                                                                                        
       var &var1. &var2.;                                                                                                   
       where &var3. ;                                                                                                       
    run;                                                                                                                    
                                                                                                                            
    %mend class;                                                                                                            
                                                                                                                            
                                                                                                                            
    %class (var1=weight,var2=age,var3=%nrstr(&var2 ge 14 and sex = "M"));                                                   
                                                                                                                            
                                                                                                                            
                                                                                                                            
                                                                                                                            
    2. Single quotes (reminds you that you have to unquote)                                                                 
    --------------------------------------------------------                                                                
                                                                                                                            
    %macro class (var1=,var2=,var3=);                                                                                       
                                                                                                                            
    %let var3=%sysfunc(dequote(&var3));                                                                                     
                                                                                                                            
    proc print data = sashelp.class;                                                                                        
       var &var1. &var2.;                                                                                                   
       where &var3. ;                                                                                                       
    run;                                                                                                                    
                                                                                                                            
    %mend class;                                                                                                            
                                                                                                                            
    %class (var1=weight,var2=age,var3='&var2 ge 14 and sex = "M"');                                                         
                                                                                                                            
                                                                                                                            
