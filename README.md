# utl_include_code_into_sas_data_step
Include meta data code into SAS data step

    ```  Include meta data code into SAS data step                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```    INPUT                                                                                                                                                      ```
    ```    =====                                                                                                                                                      ```
    ```    WORK.META total obs=1                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```               CODE                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```      sex = "M" and age > 14                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      SASHELP.CLASS total obs=19                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      NAME       SEX    AGE    HEIGHT    WEIGHT                                                                                                                ```
    ```                                                                                                                                                               ```
    ```      Alfred      M      14     69.0      112.5                                                                                                                ```
    ```      Alice       F      13     56.5       84.0                                                                                                                ```
    ```      Barbara     F      13     65.3       98.0                                                                                                                ```
    ```      Carol       F      14     62.8      102.5                                                                                                                ```
    ```      Henry       M      14     63.5      102.5                                                                                                                ```
    ```     ....                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```    WORKING CODE  (Two solutions. This is one of them)                                                                                                         ```
    ```    ===================================================                                                                                                        ```
    ```                                                                                                                                                               ```
    ```        set meta;                                                                                                                                              ```
    ```        rc=dosubl('                                                                                                                                            ```
    ```           data want;                                                                                                                                          ```
    ```              set sashelp.class(where=('!!code!!'));                                                                                                           ```
    ```        ');                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```   OUTPUT                                                                                                                                                      ```
    ```   =======                                                                                                                                                     ```
    ```       WORK.WANT total obs=3                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```          NAME      SEX    AGE    HEIGHT    WEIGHT                                                                                                             ```
    ```                                                                                                                                                               ```
    ```         Philip      M      16     72.0       150                                                                                                              ```
    ```         Ronald      M      15     67.0       133                                                                                                              ```
    ```         William     M      15     66.5       112                                                                                                              ```
    ```    ...                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://stackoverflow.com/questions/47200766/sas-include-code-into-data-step                                                                                 ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data meta;                                                                                                                                                   ```
    ```    input code $32.;                                                                                                                                           ```
    ```  cards4;                                                                                                                                                      ```
    ```  sex = "M" and age > 14                                                                                                                                       ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  sashelp.class                                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data _null_;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```    set meta;                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```    rc=dosubl('                                                                                                                                                ```
    ```       data want;                                                                                                                                              ```
    ```          set sashelp.class(where=('!!code!!'));                                                                                                               ```
    ```       run;quit;                                                                                                                                               ```
    ```    ');                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  SECOND SOLUTION                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  %symdel code / nowarn; * just in case;                                                                                                                       ```
    ```  data _null_;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```    set meta;                                                                                                                                                  ```
    ```    call symputx('code',code);                                                                                                                                 ```
    ```    rc=dosubl('                                                                                                                                                ```
    ```       data want;                                                                                                                                              ```
    ```          set sashelp.class(where=(&code.));                                                                                                                   ```
    ```       run;quit;                                                                                                                                               ```
    ```    ');                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  run;quit;                                                                                                                                                    ```

