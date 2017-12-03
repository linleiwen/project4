### Count by SR Type
    SELECT Service_type.sr_type_code, Service_type.sr_description, COUNT(*) AS count
    FROM facts
    JOIN Service_type ON facts.Service_type_key = Service_type.Service_type_key
    GROUP BY 1,2
    ORDER BY count DESC
    LIMIT 10;

### Count records of different month by type
    SELECT hour.month_of_year_str, COUNT(*) AS count
    FROM facts
    JOIN hour ON facts.created_date_key = hour.hour_key
    GROUP BY 1
    ORDER BY count DESC;

    SELECT hour.month_of_year_str AS month, Service_type.sr_description, COUNT(*) AS count
    FROM facts
    JOIN hour ON facts.created_date_key = hour.hour_key
    JOIN Service_type ON facts.Service_type_key = Service_type.Service_type_key
    WHERE hour.month_of_year = 6
    GROUP BY 1,2
    ORDER BY count DESC
    LIMIT 5;


这个地方我想加个loop,来看每个月的top 5 types，但搞了半天也没弄出来，所以就先用where = 来一个个看了，这里只写了6月份（记录最多的）

### Count by Department
    SELECT Service_type.owning_department, COUNT(*) AS count
    FROM facts 
    JOIN Service_type ON facts.Service_type_key = Service_type.Service_type_key
    GROUP BY owning_department
    ORDER BY count DESC
    LIMIT 10;
### Count by Dep and year
    SELECT hour.year, Service_type.owning_department, COUNT(owning_department) AS count
    FROM facts 
    JOIN Service_type ON facts.Service_type_key = Service_type.Service_type_key
    JOIN hour ON facts.created_date_key = hour.hour_key
    GROUP BY year, owning_department
    ORDER BY year, count DESC;
    

### Count by Dep and year and month(我对上上面一个做了修改，只针对top 5 popular department 做count)
    SELECT hour.year, hour.month_of_year,  Service_type.owning_department, COUNT(owning_department) AS count
    FROM facts 
    JOIN Service_type ON facts.Service_type_key = Service_type.Service_type_key
    JOIN hour ON facts.created_date_key = hour.hour_key
    Where Service_type.owning_department = 'Austin Code Department'
    OR Service_type.owning_department = 'Animal Services Office'
    OR Service_type.owning_department ='Austin Resource Recovery'
    OR Service_type.owning_department ='Transportation'
    OR Service_type.owning_department ='Public Works'
    GROUP BY 1,2, owning_department
    ORDER BY 1,2, count DESC;
