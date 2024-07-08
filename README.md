# SQL-Analysis
Education for All Fundraising is a charity organization, the Head of the Organization asked my team to present the data on donor insights and donation rates. Objectives of the organization are to:  • Increase the number of donors in your database  • Increase the donation frequency of your donors. • Increase the value of donations in your database. 

select * from donation_data
select * from donor_data

--Question a. How much is the total donation
select 
sum(donation) as Total_Donation
from donation_data;

--Question b. What is the total donation by gender?
select gender, 
	sum(donation) as Total_Donation
from donation_data
group by gender;

--Question c. Show the total donation and number of donation by gender
select gender,
	sum(donation) as Total_Donation,
	count(donation) as Number_of_Donations
from donation_data
group by gender;

--Question d. Total donation made by frequency of donation
select dr.donation_frequency,
	sum(dn.donation) as Total_Donation
from donor_data dr
join donation_data dn on dr.id = dn.id
group by dr.donation_frequency;

--Question e. Total donation and number of donation by job field
select job_field, 
	sum(donation) as Total_Donation,
	count(donation) as Number_of_Donation
from donation_data
group by job_field;

--Question f. Total donation and number of donations above $200
select
	sum(donation) as Total_Donation,
	count(donation) as Number_of_Donation
from donation_data
where donation > 200;

--Question g.  Total donation and number of donations below $200
select
	sum(donation) as Total_Donation,
	count(donation) as Number_of_donation
from donation_data
where donation < 200;

--Question h. Which top 10 States contributes the highest donations
select state,
	sum(donation) as Total_Donation
from donation_data
group by state
order by Total_Donation desc
limit 10;

--Question i.  Which top 10 States contributes the least donations
select state,
	sum(donation) as Total_Donation
from donation_data
group by state
order by Total_Donation
limit 10;

--Question j. What are the top 10 cars driven by the highest donors
select dr.car,
	sum(dn.donation) as Total_Donation
from donation_data dn
join donor_data dr on dn.id = dr.id
group by dr.car
order by Total_Donation desc
limit 10;

--Further Analysis. 10 Individuals that made highest donation
select first_name,last_name,gender,
	sum(donation) as Total_donation,
	coalesce(university,'No University') as Tertiary_Institution
from donation_data
join donor_data on donation_data.id = donor_data.id
group by first_name,last_name,gender,university
order by Total_donation desc
limit 10;

--Further Analysis. 10 Individuals that made least donation
select first_name,last_name,gender,
	sum(donation) as Total_donation,
	coalesce(university,'No University') as Tertiary_Institution
from donation_data
join donor_data on donation_data.id = donor_data.id
group by first_name,last_name,gender,university
order by Total_donation 
limit 10;

--Further Analysis. Individuals with donation between $300 & $305
select first_name,last_name,state,job_field,
	sum(donation) as Total_donation,
	coalesce(university,'No University') as Tertiary_Institution
from donor_data
join donation_data on donor_data.id = donation_data.id
where donation between 300 and 305
group by first_name,last_name,state,job_field,university,second_language
order by Total_donation asc














