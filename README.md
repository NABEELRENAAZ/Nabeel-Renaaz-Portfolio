1ST QUERY

Calculate Total Food Sales Across All Venues For Comparison.

  SELECT
   Venue.Venue_ID AS 'Venue ID',
   Venue.Venue_Name AS 'Venue Name',
   SUM(Food.Food_Price * Food_Order.Quantity_Sold) AS ' Sales'
  FROM
   TEST.Venue
  INNER JOIN
   TEST.Venue_Table
  ON
   Venue.Venue_ID = Venue_Table.Venue_ID
  INNER JOIN
   TEST.Item_Order
  ON
   Venue_Table.Table_ID = Item_Order.Table_ID
  INNER JOIN
   TEST.Food_Order
  ON
   Item_Order.Order_ID = Food_Order.Order_ID
  INNER JOIN
   TEST.Food
  ON
   Food_Order.Food_ID = Food.Food_ID
  GROUP BY
   Venue.Venue_ID,
   Venue.Venue_Name
  ORDER BY
   Sales DESC;



2nd QUERY
Find Out The Employees That Are Working In A Particular Venue, During A Particular Shift. This could help them Manage
Staff shifts in any case they have any changes to make or instructions for staff working in that particular shift.

SELECT
  Staff.Staff_ID AS 'Staff ID',
  CONCAT(Staff.Staff_Fname, ' ', Staff.Staff_Lname) AS 'Staff Name',
  Staff.Staff_Designation AS 'Designation'
FROM
  Staff
INNER JOIN
  TEST.Staff_Shift
ON
  Staff.Staff_ID = Staff_Shift.Staff_ID
AND
  Staff_Shift.Shift_ID = 'MSWE1'
AND
   Staff.Venue_ID = '46';


3rd QUERY
Price Discounted at 30% off for Non-Alchoholic Drinks when orders for more than 2 are made.

SELECT
 Drink_Order.Order_ID AS 'Order ID',
 Drink.Drink_ID AS ' Drink ID',
 Drink.Drink_Name AS ' Drink Name',
 ROUND(Drink.Drink_Price * 0.7,2) AS 'Discounted Price'
FROM
 TEST.Drink
INNER JOIN
 TEST.Drink_Order
ON
 Drink.Drink_ID = Drink_Order.Drink_ID
AND
 Quantity_Sold >= 2
AND
 Drink.Drink_Type = 'Alchoholic' ;


4th QUERY
Find out which Staff member is given a particular perk, in this case a company car, bringing back details of the employee for Crazy Cat in any case the
car needs to be handed over on demand to them. And to be more specific, a member working in a specific venue.

SELECT
  Staff.Staff_ID AS 'ID',
  CONCAT(Staff.Staff_FName, ' ' , Staff.Staff_Lname) AS 'Staff Name',
  Staff.Staff_Contact AS 'Contact Number',
  Staff.Staff_Email AS 'Email'
FROM
  TEST.Staff
INNER JOIN
  TEST.Full_Time_Staff
ON
  Staff.Staff_ID = Full_Time_Staff.Staff_ID
AND
  Full_Time_Staff.Staff_Perk LIKE '%Company Car%'
AND
  Staff.Venue_ID = '46' ;


5TH QUERY
Increased Wage Value after a 40% Wage bonus for Part_Time_Staff working on a Sunday

SELECT
  Part_Time_Staff.Staff_ID
AS
  'Staff ID', ROUND(Part_Time_Staff.Wage * 1.4,2)
AS
  'Wage'
FROM
  TEST.Part_Time_Staff
INNER JOIN
  TEST.Staff
ON
  Part_Time_Staff.Staff_ID = Staff.Staff_ID
AND
  Staff.Working_Days LIKE '%Sunday%'
ORDER BY
  Wage DESC;
