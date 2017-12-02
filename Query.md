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
