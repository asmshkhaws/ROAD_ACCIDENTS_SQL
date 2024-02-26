#  ROAD ACCIDENT SQL QUERIES

**Author**: Asim Ejaz Sheikh <br />
**Email**: asm.shkh@gmail.com <br />
**Website**: https://asmshkhaws.github.io/Data_Analyst_Website/ <br />

:exclamation: If you find this repository helpful, please consider giving it a :star:. Thanks! :exclamation:


A. KPI’s

1. Total Casualties Current Year(2022):
    
        Select sum(number_of_casualties) as CY_Casualties
        From road_accident
        Where YEAR(accident_date) = '2022'
        
   Output:
    |CY_Casualties|
    |:----|
    |195737|

2. Current Year(2022) Accidents

        Select Count(Distinct accident_index) as CY_Accidents
        From road_accident
        Where YEAR(accident_date) = '2022'

    Output:
    |CY_Accidents|
    |:----|
    |144419|

3. Total Fatal Casualties taken place Current Year(2022)
   
        Select Sum(number_of_casualties) as CY_Fatal_Casualties
        From road_accident
        Where YEAR(accident_date) = '2022' AND accident_severity = 'Fatal'

    Output:
    |CY_Fatal_Casualties|
    |:----|
    |2855|

    --Total % of Fatal Casualties taken place
   
        Select Cast(Cast(Sum(number_of_casualties) As decimal (10,2))*100 
        / (Select Cast(Sum(number_of_casualties) As decimal (10,2)) from road_accident) as decimal(10,2)) as PCT
        From road_accident
        Where accident_severity = 'Fatal'
   
    Output:
    |PCT|
    |:----|
    |1.71|

4. Total Serious Casualties taken place Current Year(2022)
   
        Select Sum(number_of_casualties) as CY_Serious_Casualties
        From road_accident
        Where YEAR(accident_date) = '2022' AND accident_severity = 'Serious' 

    Output:
    |CY_Serious_Casualties|
    |:----|
    |27045|

   --Total % of Serious Casualties taken place
   
        Select Cast(Cast(Sum(number_of_casualties) As decimal (10,2))*100 
        / (Select Cast(Sum(number_of_casualties) As decimal (10,2)) from road_accident) as decimal(10,2)) as PCT
        From road_accident
        Where accident_severity = 'Serious'

    Output:
    |PCT|
    |:----|
    |14.19|

5. Total Slight Casualties taken place Current Year(2022)
   
        Select Sum(number_of_casualties) as CY_Slight_Casualties
        From road_accident
        Where YEAR(accident_date) = '2022' AND accident_severity = 'Slight' 

    Output:
    |CY_Slight_Casualties|
    |:----|
    |165837|

   --Total % of Slight Casualties taken place
   
        Select Cast(Cast(Sum(number_of_casualties) As decimal (10,2))*100 
        / (Select Cast(Sum(number_of_casualties) As decimal (10,2)) from road_accident) as decimal(10,2)) as PCT
        From road_accident
        Where accident_severity = 'Slight'

    Output:
    |PCT|
    |:----|
    |84.10|

6. Casualties by Vehicle_Type Current Year(2022)
   
   --SELECT DISTINCT vehicle_type FROM road_accident ORDER BY vehicle_type;


          Select
            CASE
                When vehicle_type in ('Agricultural vehicle') then 'Agricultural'
                When vehicle_type in ('Bus or coach (17 or more pass seats)', 'Minibus (8 - 16 passenger seats)') then 'Bus'
                When vehicle_type in ('Car', 'Taxi/Private hire car') then 'Car'
                When vehicle_type in ('Motorcycle 125cc and under', 'Motorcycle 50cc and under', 'Motorcycle over 125cc and up to 500cc', 'Motorcycle over 500cc', 'Pedal cycle') then 'Bike'
                When vehicle_type in ('Goods 7.5 tonnes mgw and over', 'Goods over 3.5t. and under 7.5t', 'Van / Goods 3.5 tonnes mgw or under') then 'Van'
                Else 'Other'
            End as vehicle_group,
            Sum(number_of_casualties) AS CY_Casualties
          From road_accident
          Where YEAR(accident_date) = '2022'
          Group by
            CASE
                When vehicle_type in ('Agricultural vehicle') then 'Agricultural'
                When vehicle_type in ('Bus or coach (17 or more pass seats)', 'Minibus (8 - 16 passenger seats)') then 'Bus'
                When vehicle_type in ('Car', 'Taxi/Private hire car') then 'Car'
                When vehicle_type in ('Motorcycle 125cc and under', 'Motorcycle 50cc and under', 'Motorcycle over 125cc and up to 500cc', 'Motorcycle over 500cc', 'Pedal cycle') then 'Bike'
                When vehicle_type in ('Goods 7.5 tonnes mgw and over', 'Goods over 3.5t. and under 7.5t', 'Van / Goods 3.5 tonnes mgw or under') then 'Van'
                Else 'Other'
            End

    Output:
    |vehicle_group|CY_Casualties|
    |:----|:----|
    |Other|1446|
    |Agricultural|399|
    |Car|155804|
    |Bike|15610|
    |Van|15905|
    |Bus|6573|

7. Monthly Casualties in Current Year(2022)
   
        Select DATENAME(Month, accident_date) as Month_Name, Sum(Number_of_casualties) AS CY_Casualties
        From road_accident
        Where YEAR(accident_date) = '2022'
        Group by DATENAME(Month, accident_date)

   Output:
    |Month_Name|CY_Casualties|
    |:----|:----|
    |October|18287|
    |July|17201|
    |November|18439|
    |August|16796|
    |May|16775|
    |September|17500|
    |February|14804|
    |January|13163|
    |April|15767|
    |March|16575|
    |December|13200|
    |June|17230|


-- Monthly Casualties in Previous Year(2021)

        Select DATENAME(Month, accident_date) as Month_Name, Sum(Number_of_casualties) AS PY_Casualties
        From road_accident
        Where YEAR(accident_date) = '2021'
        Group by DATENAME(Month, accident_date)

  Output:
  |Month_Name|PY_Casualties|
  |:----|:----|
  |February|14648|
  |March|17815|
  |December|18576|
  |October|20109|
  |July|19682|
  |November|20975|
  |August|18797|
  |January|18173|
  |April|17335|
  |June|18728|
  |May|18852|
  |September|18456|

8. Casualties by Road_Type in Current Year(2022)
   
        Select road_type, Sum(number_of_casualties) as CY_Casualties
        From road_accident
        Where YEAR(accident_date) = '2022'
        Group by road_type

  Output:
  |road_type|CY_Casualties|
  |:----|:----|
  |Roundabout|12683|
  |Slip road|2990|
  |Dual carriageway|31912|
  |One way street|3499|
  |Single carriageway|144653|

9. % Casualties by Urban/Rural in Current Year(2022)

        Select urban_or_rural_area, Cast(Cast(Sum(number_of_casualties) as decimal (10,2))*100
        /(Select Cast(Sum(number_of_casualties)as decimal (10,2)) from road_accident) as decimal (10,2)) as CY_Casualties
        From road_accident
        Where YEAR(accident_date) = '2022'
        Group by urban_or_rural_area

  Output:
  |urban_or_rural_area|CY_Casualties|
  |:----|:----|
  |Rural|17.82|
  |Urban|29.02|

10. % Casualties by Light Condition in Current Year(2022)
    
--Select Distinct light_conditions from road_accident order by light_conditions

        Select
        	Case
        		When light_conditions in ('Darkness - lighting unknown', 'Darkness - lights lit', 'Darkness - lights unlit', 'Darkness - no lighting') then 'Night'
        		Else 'Day'
        	End as light_condition,
        	Cast(Cast(Sum(number_of_casualties) as decimal (10,2))*100
        /(Select Cast(Sum(number_of_casualties)as decimal (10,2)) from road_accident Where YEAR(accident_date) = '2022') as decimal (10,2)) as CY_Casualties
        From road_accident
        Where YEAR(accident_date) = '2022'
        Group by
        	Case
        		When light_conditions in ('Darkness - lighting unknown', 'Darkness - lights lit', 'Darkness - lights unlit', 'Darkness - no lighting') then 'Night'
        		Else 'Day'
        	End

  Output:
  |light_condition|CY_Casualties|
  |:----|:----|
  |Night|26.16|
  |Day|73.84|
11. Top 10 Casualties by Location
    
        Select Top 10 local_authority, Sum(number_of_casualties) as Total_Casualties
        From road_accident
        Group by local_authority
        Order by Total_Casualties Desc

  Output:
  |local_authority|Total_Casualties|
  |:----|:----|
  |Birmingham|8611|
  |Leeds|5821|
  |Bradford|4431|
  |Manchester|4366|
  |Liverpool|4052|
  |Cornwall|3820|
  |Sheffield|3737|
  |Kirklees|3312|
  |County Durham|3295|
  |Westminster|3169|

