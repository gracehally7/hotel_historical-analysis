# hotel_historical-analysis



create table year_revenue(
hotel varchar,
is_cancelled int,
lead_time int,
arrival_date_year int,
arrival_date_month varchar,
arrival_date_week_number int,
arrival_date_day_of_month int,
stays_in_weekend_nights int,
stays_in_week_nights int,
adults int,
children int,
babies int,
meal text,
country text,
market_segment varchar,
distribution_channel varchar,
is_repeated_guest int,
previous_cancellations int,
previous_bookings_not_cancelled int,
reserved_room_type text,
assigned_room_type text,
booking_changes int,
deposit_type text,
agent varchar,
company varchar,
days_in_waiting_list int,
customer_type varchar,
adr varchar,
required_car_parking_spaces int,
total_of_special_requests int,
reservation_status varchar,
reservation_status_date date);
alter table year_revenue alter column children type varchar;

--inserting values into the tables--
copy year_revenue from 'C:\Program Files\PostgreSQL\hotel_data\hotel_2018.csv' CSV header;
copy year_revenue from 'C:\Program Files\PostgreSQL\hotel_data\hotel_2019.csv' CSV header;
copy year_revenue from 'C:\Program Files\PostgreSQL\hotel_data\hotel_2020.csv' CSV header;
 
 select * from year_revenue;
 
 --creating meal table--
 create table meal_cost (
 cost varchar,
 meal varchar);
 copy meal_cost from 'C:\Program Files\PostgreSQL\hotel_data\meal_cost.csv' CSV header;
 
 --create market_segment table--
 create table market_segment(
 Discount varchar,
 market_segment varchar);
 copy market_segment from 'C:\Program Files\PostgreSQL\hotel_data\market_segment.csv' CSV header;
 
 
 --joining the three tables together--
select a.meal,a.cost ,sm.* from meal_cost as a
join ( select s.*,m.discount,m.market_segment 
	  from year_revenue as s 
	  left join market_segment as m on s.market_segment =m.market_segment )as sm
on a.meal= sm.meal;
