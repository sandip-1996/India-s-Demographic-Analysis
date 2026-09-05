# DEMOGRAPHIC ANALYSIS – 
## NEW PYTHON LEARNING – 
1. 	**FOR REMOVING ROW –**
	DATA.COLUMNS = DATA.ILOC[15]; 				                                                                
        DATA = DATA.ILOC[16:].RESET_INDEX(DROP=TRUE)

2. 	CHECKING DATA CONTAIN SPACE OR NOT – 
	PRINT(REPR(DATA[COLUMN1].ILOC[0] ))

3. 	STORING COLUMN AS LIST WHICH CONTAIN SPACE – 
	COLUMN_CONTAINED_SPACE = [COL FOR COL IN DATA.COLUMNS IF DATA[COL].ASTYPE(STR).STR.CONTAINS(R"\S+").ANY()] 
        # ANY() FUNCTION CHECK WHOLE COLUMN IF ANY ONE VALUE IS TRUE IT FLAGGED THAT COLUMN AS TRUE OTHERWISE FALSE

4. 	CONVERT DATA INTO STRING AND REMOVE SPACE AND FLAGGED AS NUMERIC - 
	FOR COLUMN IN COLUMN_CONTAINED_SPACE -  
        # DATA[COLUMN] = (DATA[COLUMN].ASTYPE(STR).STR.REPLACE(R"\S+","",REGEX=TRUE))  
        ASTYPE(STR) CONVERT THE DATA INTO STRING, REGEX = TRUE MEANS IT IS REGULAR EXPRESSION NOT PLAIN TEXT. 
        DATA[COLUMN] = PD.TO_NUMERIC(DATA[COLUMN], ERRORS = 'COERCE') # COERCE FLAGGED ANY ERROR AS NAN

5.      CREATE METADATA ALOGORITM FOR MAKING ABBRIVIATIONS OF COLUMN'S NAME - 
        CREATE STOP WORDS, STOP NUMBERS AND CLEANED ALL THE COLUMN ONE BY ONE,
        SPLIT INTO WORDS LIST EXCLUDING STOP_WORDS, 
        STRING CONCATINATION DONE ON FIRST LETTER OF EVERY WORDS WITH NUMBERS 

6.      HOW TO CLEAN DATA BY REGULAR EXPRESSION AND BY CONVERTING NUMERIC
        SYNTAX -> is_invalid = data[data['COL'].astype(str).str.contains(r'[^0-9.]', na=False)]
        BY NUMERIC -> 
                CHECKING THE NULL VALUES
                is_invalid = pd.to_numeric(data['COL'], errors='coerce').isna() & data['COL'].notna()  -> TRUE & FALSE
                invalid_rows = data[is_invalid] 
                invalid_rows['Total Fertility Rate (live births per woman)'].unique()
                DROP THE ROW 
                data[col] = pd.to_numeric(data[col], errors='coerce')
                data = data.dropna(subset=[col])

7.      DIFFERENCE BETWEEN TUPLE AND LIST
        TUPLE = (MIXED DATA TYPE)       |       LIST = [MIXED DATA TYPE]
        t = ([1, 2], 3)
        t[0] = [4, 5]   # ❌ TypeError (can't reassign tuple element)
        t[0][0] = 99    # ✅ Works (modifying list inside tuple)
        spect	        List	                        Tuple
        Performance	Slower (more overhead)	        Faster (lightweight)
        Memory	        Uses more memory	        Uses less memory
        Use Case	Dynamic data (changes often)	Fixed data (never changes)
        Methods	Many    (append, pop, sort, etc.)	Few (count, index)
        Hashable?	❌ No (can't be dict key)       ✅ Yes (if all elements hashable)
        Iteration	Slightly slower	                Slightly faster

8.      columns_list = {key: key.replace(" ","_") for key in data.columns}
        or 
        keys = ()
        values = ()
        for key in data.columns:
        value = key.replace(" ", "_")
        keys += (key,)
        values += (value,)
        column_list = dict(zip(keys, values))

9.      HOW TO INVERT KEY VALUE TO VALUE KEY. 
        INV = DICT(ZIP(ORGINIAL_DICT.VALUES(), ORIGINAL_DICT.KEYS())) # it will replace identical values with latest values. to keep it another approach
        ------------
        from collections import defaultdict
        inv = defaultdic(list)
        for key, value in original_dict.items():
                inverted_dict[value].append(key)
        print(dict(inverted_dict))

10.     SORT KEYS USING VALUES IN DICT = {KEYS STR: VALUES NUMERICAL}
        SORTED_KEYS = sorted(dict, key=dict.get, reverse = True) # reverse = True for descending order


11.     USING GROUPBY METHOD
        DATA.GROUPBY('Mcolumn to group by')['column to calculate'].count() # ignore NaN value, so .size() included NaN value. 
        CHECKING UNIQUE VALUES
        data.groupby('column to group by')['column to calculate'].nunique()
        or
        data.groupby('column to group by')['column to calculate'].agg(['nunique',list]).query('nunique > 1').sort_values('nunique', ascending=False)
        or 
        data.groupby('column to group by')[['column1', 'column2']].nunique().query('column1 > 1 or column2 > 1').sort_values(['column1', 'column2'], ascending=False)


12.     CHECKING DUPLICATE ROWS
        DATA[DATA.DUPLICATED()]; IF EMPTY DATAFRAME NO DUPLICATE; 
        DATA[].DUPLICATED().SUM()
        DATA[].DUPLICATED(KEEP = FALSE) # keep = false; it will identify all records that are duplicate

13.     arbitary inf float point for first comparisions wins. -> float('inf')

14.     if __name__ == '__main__':  it means run this code when executed directly

15.     data.fillna({col: "text"}, inplace = True)

16.     int64 and Int64 both are different datatype. int64 this is numpy 64 bit integer type. it has no representation for NaN. Int64 is pandas nullable integer. pandas uses pd.na to represent missing values. 

17.     str and string both are different datatype. astype('str') convert every value to string including null values. astype('string') convert string but keep null values same. 

18.     USING REGEX PATTERNS: 
                Opening Delimiter + (Negated Class)*  + Closing Delimiter
                Examples:
                Text inside double quotes "...":
                r'"([^"]*)"'

                Text inside square brackets [...]:
                r'\[([^\]]*)\]'

                Text inside HTML tags <...>:
                r'<([^>]*)>'

                \( and \) match the literal outer parentheses (not captured).
                ([^)]*) capture group (...) containing "anything except ) repeated zero or more times."

                \( literal opening parenthesis
                [^)]* any characters that are not a closing parenthesis
                \) literal closing parenthesis
                \s* zero or more spaces after
                \s+ one or more spaces after

                -?\\d+\\.\\d+  --> -? optional negetive sign; ? means optional
                \\d+ --> numbers one or more 
                . -> means match any single character 
                \\.  -> macth an actual . dot character
                (...)      → group AND remember it
                (?:...)    → group but DON'T remember it
                (?:...)?   -> group but don't remember it optional

19.     how to make dataframe: 
        dict = {'key1': value, 'key2': value}
        df = pd.DataFrame(dict)

20.     result = grouped['TEST CODE'].agg('+'.join)
                > ["REFE", "REFT", "SFCM"]
                > "REFE+REFT+SFCM"
21.     (data1.columns.str.replace('\xa0', ' ', regex=False).str.strip()) replace this special space

22.     date_check = pd.to_datetime(data1["DUE DATE"], dayfirst=True, errors="coerce"); date_check.isna().sum()

23.     folder = Path(path, "files")
        files = list(folder.glob('*.csv'))
        upload more than 1 number of files. 
        for file in files:
                ---- 


DATA PARSING FROM WEB
1.      TABLE DOWNLOAD FROM WIKIPEDIA USING PANDAS
        404 ERROR : WIKIPEDIA DOESNOT ALLOW PANDAS TO GET DATA, USE HEADER

2.      

SQL LEARNING POSTGRE 
1.      UNION TWO TABLE COLUMN BY COLUMN - 
        (...) UNION (...)

2.      CALCULATE MEDIAN - 
        SELECT PERCENTILE__CONT(0.5) WITHIN GROUP (ORDER BY COLUMN1) AS COLUMN_NAME FROM TABLE1

3.      SET COLUMN DOUBLE PRECISION VALUE ROUNDED UPTO 2 DECIMAL 
        UPDATE TABLE1 SET COLUMN1 = ROUND(COLUMN1::NUMERIC, 2) # ROUND DOESNOT WORK WITH DOUBLE PRECISION SO WE NEED TO CHANGE IT INTO NUMERIC

4.      CREATE A TABLE VIEW
        CREATE OR REPLACE VEIW TABLE1 AS SELECT * FROM TEMP_TABLE;

5.      DROP COLUMN: 
        ALTER TABLE TABLE_NAME DROP COLUMN COLUMN_NAME1, DROP COLUMN COLUMN_NAME2...;

        ADD COLUMN: 
        ALTER TABLE TABLENAME ADD COLUMN COLUMN_NAME DATATYPE;

        UPDATE COLUMN:
        UPDATE TABLE SET COLUMN = ...... ;

6.      DROP ROWS:
        DELETE FROM TABLE_NAME WHERE .... 

        DELETE TABLE: 
        DROP TABLE TABLE_NAME; 
        TRUNCATE TABLE TABLE

7.      DROP VIEW: 
        DELETE VIEW TABLE_NAME 

8.      STORE ROW_NUMBER BY PARTITION: 
        WRONG SQL - 
                SELECT LOCATION, TFR, ROW_NUMBER() OVER(PARTITION BY TFR_GROUP ORDER BY TFR DESC) AS RANK
                FROM LOW_TFR_COUNTRIES WHERE RANK = 1
                ((RANK PERFORM FIRST THEN SELECT, IT THROWS ERROR))
        CORRECT SQL - 
        WITH RankedData AS (
                SELECT 
                        LOCATION, 
                        TFR, 
                        ROW_NUMBER() OVER(PARTITION BY TFR_GROUP ORDER BY TFR DESC) AS RANK
                FROM LOW_TFR_COUNTRIES
                )
                SELECT 
                LOCATION, 
                TFR, 
                RANK
                FROM RankedData 
                WHERE RANK = 1;
9.      SUM(COUNT(*)) OVER(): 
         WE CANNOT USE SUM OVER ALREADY AGGRIGATED FUNCITON. HERE COUNT(*) IS ALREADY AGGRIGATED. SUM(COUNT(*)) WILL THROW AN ERROR.
         SUM(*)  OUTPUT WILL BE ONE ROW. ALL ROWS COLLAPESED INTO ONE ROW. 
         SUM(COUNT(*)) OVER() OUTPUT WILL BE EVERY ROW, CALCULATE THE SUM BUT DONOT COLLAPES THE ROWS. 

POWERBI - 
1.      DAX FORMAT FOR CHANGING METRIC SYSTEM FROM MILLION BILLION TO CRORE AND LAKH FORMAT.
        Births in Lakhs/Crores =
        VAR CurrentValue = SUM('Table'[Column])
        RETURN
                SWITCH(
                        TRUE(),
                        CurrentValue >= 10000000, FORMAT(CurrentValue / 10000000, "0.00 Cr"),
                        CurrentValue >= 100000, FORMAT(CurrentValue / 100000, "0.00 L"),
                        CurrentValue >= 1000, FORMAT(CurrentValue / 1000, "0.00 K"),
                        FORMAT(CurrentValue, "#,##0") here "#,##0" is thousand seperator
        )

2.      POWERBI CONCEPT: 
        FORMAT() -> RETURN TEXT NOT NUMBER; CONVERTS STRINGS FOR DISPLAY PURPOSES. 
                EX - FORMAT((COL1 + COL2)/2,"0.00")

        DIVIDE(COL1 + COL2, 2, 0) -> HANDLES DIVISION BY ZERO

        MEASURE: USES CPU PROCESSING AND COMPUTED ON THE FLY WHEN WE INTERACT WITH REPORT
                RETURN A SINGLE AGGRIGATED VALUE
                USED IN KPI, METRICS, RATIOS, PERCENTAGE, COMPARISIONS
                CHANGE WITH FILTER


        CALCULATED COLUMN: USES RAM STORAGE AND ARE COMPUTED WHEN DATA LOADS. 
                RETURN ROW LEVEL CALCULATION, FILTERING, RELATIONSHIPS
                ADDS NEW COLUMN INTO TABLE
                DOESNOT CHANGE WITH FILTER

3.      > ADD COLUMN USING POWER QUERIES:
        TRANSFORM DATA > ADD COLUMN > TABLE_NAME = Text.From(Number.IntegerDivide([year_],10)*10) & "_" & Text.From((Number.IntegerDivide([year_],10)*10)+10) > ok apply. 

        Number.IntergerDivide(col, divisor)
        ---------------------
        > SAME TASK USING DAX 
        NEW COLUMN > TABLE_NAME = 
                VAR STARTDECADE FLOOR('Mortality_data[Year_],10)
                RETURN 
                        STARTDECADE & "_" & (STARTDECADE +10)

        OUTPUT- 
        TABLE_NAME
        1950 - 1960
        1960 - 1970
        .
        ---------------------
        > CREATE SEPERATE DAX TABLE
        FIRST CREATE Decade COLUMN ON EXISTING TABLE
        Decade_MLE_Summary = 
        ADDCOLUMNS(
        SUMMARIZE(
                'Mortality_data',
                'Mortality_data'[Decade]
        ),
        "Avg_MLE", CALCULATE(AVERAGE('Mortality_data'[MLE_]))
        )

4.      SYNTAX - 
        SUMMARIZE(
                <table>,
                <groupBy_columnName1>,
                [<groupBy_columnName2>],
                ...)

        ADDCOLUMNS(
                <table>,  # caution it will take whole table
                "<Name1>", <Expression1>,
                ["<Name2>", <Expression2>],
                ...)
        )

        SELECTCOLUMNS(
                table,  # it will draw only seleccted columns return table
                "column_name", expression,
                "column_name", expression   
                )
        
        VALUES( <TableNameOrColumnName> )
                -> RETURNS COLUMN OR TABLE OF UNIQUE VALUES

        CALCULATE(AVERAGE(...), IF(...))

        SWITCH(
                <Expression>, # TRUE(   )
                <Value1>, <Result1>,
                <Value2>, <Result2>,
                ...,
                [<Else>]
                )

        LOOKUPVALUE(
                <result_column>,
                <search_column1>, <search_value1>,
                [<search_column2>, <search_value2>],
                ...
                )

        FILTER(
                <table>,
                <condition>
                )
        ## FILTER() returns a table, not a single value

        IMPORTANT OPERATORS:    
                &&    -- AND
                ||    -- OR
                =     -- equal
                <>    -- not equal
                >     -- greater than
                <     -- less than
                >=    -- greater/equal
                <=    -- less/equal

        DATATABLE(
                "ColumnName", DataType,
                {
                        {value1},
                        {value2},
                        {value3}
                }
                )

        SELECTEDVALUE(Column, AlternativeResult)

                example: Create new table disconnect table
                        AgeGroups =
                                DATATABLE(
                                "Age Group", STRING,
                                "Order", INTEGER,
                                {
                                        {"15–50", 1},
                                        {"15–60", 2},
                                        {"Before 40", 3},
                                        {"Before 60", 4}
                                }
                                )
                        Female Mortality =
                                SWITCH(
                                SELECTEDVALUE(AgeGroups[Age Group]),

                                "15–50", AVERAGE(mortality_rate[fma_15_50]),
                                "15–60", AVERAGE(mortality_rate[fma_15_60]),
                                "Before 40", AVERAGE(mortality_rate[fma_40]),
                                "Before 60", AVERAGE(mortality_rate[fma_60])
                                )
