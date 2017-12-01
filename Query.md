### Count by SR Type
SELECT Service_type.sr_type_code, Service_type.sr_description, COUNT(*) AS count
<br>
FROM facts
<br>
JOIN Service_type ON facts.Service_type_key = Service_type.Service_type_key
<br>
GROUP BY 1,2
<br>
ORDER BY count DESC
<br>
LIMIT 10;
