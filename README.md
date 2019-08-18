# utl-macro-with-dosubl-to-compute-last-day-of-month
Macro with dosubl to compute last day of month
    Problem:                                                                                              
       Given "201908" (August 2019) return "31AUG2019"                                                    
                                                                                                          
    SOAPBOX ON                                                                                            
                                                                                                          
      I feel this technique is superior to Klignon language macros.                                       
      Note dosubl has th potential to as faster or faster than a macro.                                   
      Current implementation is very slow.                                                                
                                                                                                          
       Problems with macro (without dosubl)                                                               
                                                                                                          
        a. With a macro you need to wrap all functions with a sysfunc                                     
        b. You need to remove normal datastep quotes                                                      
                                                                                                          
    SOAPBOX OFF                                                                                           
                                                                                                          
    github                                                                                                
    https://tinyurl.com/yydeq89z                                                                          
    https://github.com/rogerjdeangelis/utl-macro-with-dosubl-to-compute-last-day-of-month                 
                                                                                                          
    SAS Forum                                                                                             
    https://tinyurl.com/yyf4v24w                                                                          
    https://communities.sas.com/t5/SAS-Programming/Convert-text-to-date-in-macro/m-p/578389               
                                                                                                          
                                                                                                          
    *_                   _                                                                                
    (_)_ __  _ __  _   _| |_                                                                              
    | | '_ \| '_ \| | | | __|                                                                             
    | | | | | |_) | |_| | |_                                                                              
    |_|_| |_| .__/ \__,_|\__|                                                                             
            |_|                                                                                           
    ;                                                                                                     
                                                                                                          
    %monthEnd(201908)                                                                                     
                                                                                                          
    *            _               _                                                                        
      ___  _   _| |_ _ __  _   _| |_                                                                      
     / _ \| | | | __| '_ \| | | | __|                                                                     
    | (_) | |_| | |_| |_) | |_| | |_                                                                      
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                     
                    |_|                                                                                   
    ;                                                                                                     
                                                                                                          
    %put monthEnd=  %monthEnd(201908);                                                                    
                                                                                                          
      monthEnd = 31AUG2019                                                                                
                                                                                                          
                                                                                                          
    *          _       _   _                                                                              
     ___  ___ | |_   _| |_(_) ___  _ __                                                                   
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                  
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                 
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                 
                                                                                                          
    ;                                                                                                     
                                                                                                          
    %symdel filedate / nowarn;                                                                            
                                                                                                          
    %macro monthEnd(filedate);                                                                            
                                                                                                          
      %let rc=%sysfunc(dosubl('                                                                           
         data _null_;                                                                                     
            dte=inputn("&filedate.01","yymmdd8.");                                                        
            monthEnd=putn(intnx("month",dte ,0,"E"),"date9.");                                            
            call symputx("monthEnd",monthEnd);                                                            
         run;quit;                                                                                        
       '));                                                                                               
                                                                                                          
       &monthEnd                                                                                          
                                                                                                          
    %mend monthEnd;                                                                                       
                                                                                                          
                                                                                                          
    %put monthEnd = %monthEnd(201908);                                                                    
                                                                                                          
    or                                                                                                    
                                                                                                          
    data want;                                                                                            
                                                                                                          
       monthEnd = "%monthEnd(201908)";                                                                    
                                                                                                          
    run;quit;                                                                                             
                                                                                                          
    /*                                                                                                    
    WORK.WANT total obs=1                                                                                 
                                                                                                          
     Obs    MONTHEND                                                                                      
                                                                                                          
      1     31AUG2019                                                                                     
    */                                                                                                    
