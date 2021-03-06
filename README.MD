This is just a test demo! do not use this in production without asking permission. (inofficial)

![alt text](https://marcosraudkett.com/uploader/uploads/c21fb5d72e4935aa09ae27217dbff002.png "Preview")

```
git clone https://github.com/marcosraudkett/tallink.git
```

### Usage
```php
<?php
  require_once 'classes/Tallink.class.php';
  /* or use autoloader */
?>
```


### Journeys
```php
<?php

/* fetch journeys from tallinn to helsinki between dateFrom and dateTo */
$fetch_journeys = new Tallink();
  $fetch_journeys->from = 'tal';
  $fetch_journeys->to = 'hel';
  $fetch_journeys->oneWay = true;
  $fetch_journeys->locale = 'en';
  $fetch_journeys->voyageType = 'SHUTTLE';
  $fetch_journeys->dateFrom = '2018-12-15'; /* from date */
  $fetch_journeys->dateTo = '2018-12-18'; /* to date */
$fetch_journeys = Tallink::fetch_journeys($fetch_journeys);

foreach($fetch_journeys as $row)
{
	echo '<br>'.$row["shipCode"]; /* prints out each journey's shipCode */
}

/* 
List of data you can print:

- "arrivalIsoDate"
- "cityFrom"
- "cityTo"
- "departureIsoDate"
- "duration"
- "hasRoom"
- "isDisabled"
- "isOvernight"
- "isVoucherApplicable"
- "marketingMessage"
- "personPrice"
- "pierFrom"
- "pierTo"
- "pointsPrice"
- "sailId"
- "sailPackageCode"
- "sailPackageName"
- "shipCode"
- "vehiclePrice"

*/

?>
```

### Land services 

```php
<?php
$fetch_land_services = new Tallink();
  $fetch_land_services->locale = 'en'; /* locale */
  $fetch_land_services->country = ''; /* country */
  $fetch_land_services->outwardSailId = '1633780'; /* outwardSailId */
$fetch_land_services = Tallink::fetch_land_services($fetch_land_services);

foreach($fetch_land_services as $row)
{
	echo $row["title"].'<br>'; /* prints each land service title for that trip */
	echo $row["description"].'<br>'; /* prints each land service description for that trip */
}

/* 
List of data you can print:

- "title"
- "imageUrl"
- "description"
- "eventTimes"

*/

?>
```

### Vehicle Prices

```php
<?php
$sailId = '1610238';
$vehiclePrice = Tallink::fetch_vehicle_prices('en', 'fi', $sailId); 

if($vehiclePrice != null) {
	foreach($vehiclePrice as $row_vechicle)
	{
		echo $row_vechicle["carCategory"]; /* prints each car category type */
		echo $row_vechicle["outwardDetails"]['availability']; /* prints each availability */
		echo $row_vechicle["outwardDetails"]['price']; /* prints each price */
	}
}

/* 
List of data you can print:

- "carCategory"
- "licensePlates"
- "outwardDetails"
- "returnDetails"

*/

?>
```

### Get station id by name 

```php
<?php
  $station_name = 'Tallinn';
  $get_station_id_by_name = Tallink::get_station_id_by_name($station_name);
  echo $get_station_id_by_name /* returns 'tal' */
?>
```

### Check if station exists

```php
<?php
  $station = 'Tallinn';
  $check_station_exists = Tallink::check_station_exists($station);
  echo $check_station_exists /* returns 1 */
?>
```
