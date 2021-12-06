---
title: GHG Emissions Calculation Tool

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript: Javascript
  - python: Python
  - php: PHP

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

HOST: [https://dynm-corporate.herokuapp.com/](https://dynm-corporate.herokuapp.com/).

## About

A calculation tool for estimating GHG emissions based on the GHG Protocol.

## How To

• Fill in company and facility information in the "Parameters" sheet. Also, provide any custom emission factors here for use in subsequent worksheets.
• The tool uses default emission factors, which vary by country. These are free to use and publicly available, and the tool includes links of where to obtain them. Currently, separate sets of emission factors are available for the UK and US. Location-based Scope 2 emission factors are also available for the US, Canada and Australia, while market-based residual mix emission factors are available for the US, Canada and all European counties.
• On the "Parameters" tab, users can supply custom emission factors, adjust the default global warming potentials and choose whether to use radiative forcing factors for air travel.
• The maximum number of facilities for this tool is 10. Additional rows cannot be added to the Facility table.
• Use each of the sheets to input inventory data for the various activities. Make sure to choose custom emission factors, if any, and to select the proper units.
• If the results don't show, please make sure that all the relevant options have been selected and that the correct Emission Factors have been chosen.
• To add more rows to any table, click on the "Insert Row" button next to the table. Do not try adding rows manually as that might affect the cell formulae.
• The GHG emissions results for each activity types are provided in the "Results Summary" sheet, with an option to print the results.
This tool covers the following cross-sectoral emission sources:
Scope 1 - Stationary Combustion, Mobile Combustion, and Fugitive Emissions from Air Conditioning
Scope 2 - Purchased Electricity and Purchased Heat/Steam
Scope 3 - Upstream Transportation and Distribution, Business Travel, and Employee Commuting

# Stationary Combustion

> REQUEST

```shell
curl --location --request POST 'https://dynm-corporate.herokuapp.com/stationary-combustion' \
--header 'Content-Type: application/json' \
--data-raw '{
  "facility_id": 1,
  "year": 2019,
  "fuel_type": "Coal Coke",
  "amount": 1000,
  "units": "therm",
  "activity_type": "Stationary combustion",
  "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
  "scope": "Scope 1"
}'
```

```javascript
const fetch = require("node-fetch");
const data = {
  facility_id: 1,
  year: 2019,
  fuel_type: "Coal Coke",
  amount: 1000,
  units: "therm",
  activity_type: "Stationary combustion",
  gwp_dataset_revision: "2014 IPCC Fifth Assessment",
  scope: "Scope 1",
};

fetch("https://dynm-corporate.herokuapp.com/stationary-combustion", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

```python
import requests
import json

url = "https://dynm-corporate.herokuapp.com/stationary-combustion"

payload = json.dumps({
  "facility_id": 1,
  "year": 2019,
  "fuel_type": "Coal Coke",
  "amount": 1000,
  "units": "therm",
  "activity_type": "Stationary combustion",
  "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
  "scope": "Scope 1"
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
<?php
  $url = "https://dynm-corporate.herokuapp.com/stationary-combustion";
  $ch = curl_init($url);
  $postData = array(
    "facility_id" => 1,
    "year"=> 2019,
    "fuel_type" => "Coal Coke",
    "amount" => 1000,
    "units" => "therm",
    "activity_type" => "Stationary combustion",
    "gwp_dataset_revision" => "2014 IPCC Fifth Assessment",
    "scope" => "Scope 1"
);

  curl_setopt_array($ch, array(
    CURLOPT_POST => TRUE, // set post data to true
    CURLOPT_RETURNTRANSFER => TRUE,
    CURLOPT_POSTFIELDS => json_encode($postData),   // post data
    CURLOPT_HTTPHEADER => array("Content-Type: application/json")
  ));

  $response = curl_exec($ch);
  curl_close ($ch);
  $data = json_decode($response, true); // decode the json response
  var_dump($data);
?>
```

> RESPONSE : <code>200</code>

```json
{
  "biofuel_c02_tonnes": 0.0,
  "c02_tonnes": 11.367,
  "c02e_tonnes": 11.4402,
  "ch4_tonnes": 0.0011,
  "ef_kg_c02e": 114.402,
  "n20_tonnes": 0.00016
}
```

Includes fuel consumption at a facility to produce electricity, steam, heat, or power. The combustion of fossil fuels by natural gas boilers, diesel generators and other equipment emits carbon dioxide, methane, and nitrous oxide into the atmosphere.

`POST https://dynm-corporate.herokuapp.com/stationary-combustion`

<aside>Request params</aside>

| Param                | Type    | Required | Description                                                       |
| -------------------- | ------- | -------- | ----------------------------------------------------------------- |
| facility_id          | integer | true     | facility id of the company                                        |
| year                 | integer | true     | the year in which the facility wants to calculate ghg emissions   |
| fuel_type            | string  | true     | type of fuel to be combusted                                      |
| amount               | number  | true     | amount of fuel to be consumed                                     |
| units                | string  | true     | units of the fuel_type to be combusted(e.g., kg or kWh or therms) |
| activity_type        | string  | true     |                                                                   |
| gwp_dataset_revision | string  | true     |                                                                   |
| scope                | string  | true     | cross-sectoral emission sources i.e scope 1, 2 and 3              |

# Mobile Combustion

> REQUEST

```shell
curl --location --request POST 'https://dynm-corporate.herokuapp.com/mobile-combustion' \
--header 'Content-Type: application/json' \
--data-raw '{
    "facility_id": 1,
    "year": 2019,
    "fuel_source": "Biodiesel (100%)",
    "vehicle_type": "Biodiesel Light-duty Vehicles",
    "amount": 100,
    "units": "scf",
    "activity_type": "Fuel Use",
    "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
    "scope": "Scope 1"
}'
```

```javascript
const fetch = require("node-fetch");
const data = {
  facility_id: 1,
  year: 2019,
  fuel_source: "Biodiesel (100%)",
  vehicle_type: "Biodiesel Light-duty Vehicles",
  amount: 100,
  units: "scf",
  activity_type: "Fuel Use",
  gwp_dataset_revision: "2014 IPCC Fifth Assessment",
  scope: "Scope 1",
};

fetch("https://dynm-corporate.herokuapp.com/mobile-combustion", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

```python
import requests
import json

url = "https://dynm-corporate.herokuapp.com/mobile-combustion"

payload = json.dumps({
  "facility_id": 1,
  "year": 2019,
  "fuel_source": "Biodiesel (100%)",
  "vehicle_type": "Biodiesel Light-duty Vehicles",
  "amount": 100,
  "units": "scf",
  "activity_type": "Fuel Use",
  "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
  "scope": "Scope 1"
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
<?php
  $url = "https://dynm-corporate.herokuapp.com/mobile-combustion";
  $ch = curl_init($url);
  $postData = array(
    "facility_id"=> 1,
    "year"=> 2019,
    "fuel_source"=> "Biodiesel (100%)",
    "vehicle_type"=> "Biodiesel Light-duty Vehicles",
    "amount"=> 100,
    "units"=> "scf",
    "activity_type"=> "Fuel Use",
    "gwp_dataset_revision"=> "2014 IPCC Fifth Assessment",
    "scope"=> "Scope 1"
);

  curl_setopt_array($ch, array(
    CURLOPT_POST => TRUE, // set post data to true
    CURLOPT_RETURNTRANSFER => TRUE,
    CURLOPT_POSTFIELDS => json_encode($postData),   // post data
    CURLOPT_HTTPHEADER => array("Content-Type: application/json")
  ));

  $response = curl_exec($ch);
  curl_close ($ch);
  $data = json_decode($response, true); // decode the json response
  var_dump($data);
?>
```

> RESPONSE : <code>200</code>

```json
{
  "biofuel_c02_tonnes": 7.069,
  "c02_tonnes": 0.0,
  "c02e_tonnes": 0.003,
  "ch4_tonnes": 6e-6,
  "ef_kg_c02e": 0.0045198,
  "n20_tonnes": 1.2e-5
}
```

Includes fuel consumption by vehicles that are owned or leased by the company. Combustion of fossil fuels in vehicles (including cars, trucks, planes, and boats) emits carbon dioxide, methane, and nitrous oxide into the atmosphere.
`POST https://dynm-corporate.herokuapp.com/mobile-combustion`

| Param                | Type    | Required | Description                                                       |
| -------------------- | ------- | -------- | ----------------------------------------------------------------- |
| facility_id          | integer | true     | facility id of the company                                        |
| year                 | integer | true     | the year in which the facility wants to calculate ghg emissions   |
| fuel_source          | string  | true     | source of fuel to be combusted                                    |
| vehicle_type         | string  | true     | type of vehicle being used                                        |
| amount               | number  | true     | amount of fuel to be consumed                                     |
| units                | string  | true     | units of the fuel_type to be combusted(e.g., kg or kWh or therms) |
| activity_type        | string  | true     |                                                                   |
| gwp_dataset_revision | string  | true     |                                                                   |
| scope                | string  | true     | cross-sectoral emission sources i.e scope 1, 2 and 3              |

# Transportation

> REQUEST

```shell
curl --location --request POST 'https://dynm-corporate.herokuapp.com/transportation' \
--header 'Content-Type: application/json' \
--data-raw '{
    "facility_id": 1,
    "year": 2019,
    "emission_dataset": "UK DEFRA",
    "vehicle_type": "Average Car - Plug-in Hybrid Electric Vehicle",
    "mode_of_transport": "Car",
    "category": "Employee Commute",
    "amount": 100,
    "units": "km",
    "activity_type": "Distance",
    "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
    "scope": "Scope 3"
}'
```

```javascript
const fetch = require("node-fetch");
const data = {
  facility_id: 1,
  year: 2019,
  emission_dataset: "UK DEFRA",
  vehicle_type: "Average Car - Plug-in Hybrid Electric Vehicle",
  mode_of_transport: "Car",
  category: "Employee Commute",
  amount: 100,
  units: "km",
  activity_type: "Distance",
  gwp_dataset_revision: "2007 IPCC Fifth Assessment",
  scope: "Scope 3",
};

fetch("https://dynm-corporate.herokuapp.com/transportation", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

```python
import requests
import json

url = "https://dynm-corporate.herokuapp.com/transportation"

payload = json.dumps({
  "facility_id": 1,
  "year": 2019,
  "emission_dataset": "UK DEFRA",
  "vehicle_type": "Average Car - Plug-in Hybrid Electric Vehicle",
  "mode_of_transport": "Car",
  "category": "Employee Commute",
  "amount": 100,
  "units": "km",
  "activity_type": "Distance",
  "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
  "scope": "Scope 3"
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
<?php
  $url = "https://dynm-corporate.herokuapp.com/transportation";
  $ch = curl_init($url);
  $postData = array(
    "facility_id"=> 1,
    "year"=> 2019,
    "emission_dataset"=> "UK DEFRA",
    "vehicle_type"=> "Average Car - Plug-in Hybrid Electric Vehicle",
    "mode_of_transport"=> "Car",
    "category"=> "Employee Commute",
    "amount"=> 100,
    "units"=> "km",
    "activity_type"=> "Distance",
    "gwp_dataset_revision"=> "2007 IPCC Fifth Assessment",
    "scope"=> "Scope 3"
);

  curl_setopt_array($ch, array(
    CURLOPT_POST => TRUE, // set post data to true
    CURLOPT_RETURNTRANSFER => TRUE,
    CURLOPT_POSTFIELDS => json_encode($postData),   // post data
    CURLOPT_HTTPHEADER => array("Content-Type: application/json")
  ));

  $response = curl_exec($ch);
  curl_close ($ch);
  $data = json_decode($response, true); // decode the json response
  var_dump($data);
?>
```

> RESPONSE : <code>200</code>

```json
{
  "biofuel_c02_tonnes": 0.011454356557703015,
  "c02_tonnes": 0.0,
  "c02e_tonnes": 1.4155457130358705e-5,
  "ch4_tonnes": 3.2932673188578697e-8,
  "ef_kg_c02e": 0.18456781,
  "n20_tonnes": 4.473872584108805e-8
}
```

Fuel consumption by vehicles used to conduct company-financed travel. Examples include commercial air travel and use of rented vehicles during business trips (travel using company-owned/leased vehicles are included in Scope 1).

`POST https://dynm-corporate.herokuapp.com/transportation`

<aside>Request params</aside>

| Param                | Type    | Required | Description                                                       |
| -------------------- | ------- | -------- | ----------------------------------------------------------------- |
| facility_id          | integer | true     | facility id of the company                                        |
| year                 | integer | true     | the year in which the facility wants to calculate ghg emissions   |
| emission_dataset     | string  | true     |                                                                   |
| vehicle_type         | string  | true     | type of vehicle being used                                        |
| mode_of_transport    | string  | true     | mode_of_transport being used e.g car                              |
| category             | string  | true     | e.g Employee Commute                                              |
| amount               | number  | true     | amount of fuel to be consumed                                     |
| units                | string  | true     | units of the fuel_type to be combusted(e.g., kg or kWh or therms) |
| activity_type        | string  | true     |                                                                   |
| gwp_dataset_revision | string  | true     |                                                                   |
| scope                | string  | true     | cross-sectoral emission sources i.e scope 1, 2 and 3              |

# Purchased Electricity

> REQUEST

```shell
curl --location --request POST 'https://dynm-corporate.herokuapp.com/electricity' \
--header 'Content-Type: application/json' \
--data-raw '{
    "facility_id": 1,
    "year": 2018,
    "emission_factor_type": "Grid Average/Location Based",
    "approach": "Purchased Electricity - Market Based",
    "amount": 100,
    "units": "GJ",
    "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
    "scope": "Scope 2",
    "facilities": [
        {
        "facility_id": 1,
        "grid_region": "AKGD",
        "country": "USA"
        },
        {
        "facility_id": 2,
        "grid_region": "Ontario",
        "country": "Canada"
        }
    ]
}'
```

```javascript
const fetch = require("node-fetch");
const data = {
  facility_id: 1,
  year: 2018,
  emission_factor_type: "Grid Average/Location Based",
  approach: "Purchased Electricity - Market Based",
  amount: 100,
  units: "GJ",
  gwp_dataset_revision: "2007 IPCC Fifth Assessment",
  scope: "Scope 2",
  facilities: [
    {
      facility_id: 1,
      grid_region: "AKGD",
      country: "USA",
    },
    {
      facility_id: 2,
      grid_region: "Ontario",
      country: "Canada",
    },
  ],
};

fetch("https://dynm-corporate.herokuapp.com/electricity", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

```python
import requests
import json

url = "https://dynm-corporate.herokuapp.com/electricity"

payload = json.dumps({
  "facility_id": 1,
  "year": 2018,
  "emission_factor_type": "Grid Average/Location Based",
  "approach": "Purchased Electricity - Market Based",
  "amount": 100,
  "units": "GJ",
  "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
  "scope": "Scope 2",
  "facilities": [
    {
      "facility_id": 1,
      "grid_region": "AKGD",
      "country": "USA"
    },
    {
      "facility_id": 2,
      "grid_region": "Ontario",
      "country": "Canada"
    }
  ]
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
<?php
  $url = "https://dynm-corporate.herokuapp.com/electricity";
  $ch = curl_init($url);
  $postData = array(
    "facility_id"=> 1,
    "year"=> 2018,
    "emission_factor_type"=> "Grid Average/Location Based",
    "approach"=> "Purchased Electricity - Market Based",
    "amount"=> 100,
    "units"=> "GJ",
    "gwp_dataset_revision"=> "2007 IPCC Fifth Assessment",
    "scope"=> "Scope 2",
    "facilities"=> [
        [
            "facility_id"=> 1,
            "grid_region"=> "AKGD",
            "country"=> "USA"
        ],
        [
            "facility_id"=> 2,
            "grid_region"=> "Ontario",
            "country"=> "Canada"
        ]
     ]
    );

  curl_setopt_array($ch, array(
    CURLOPT_POST => TRUE, // set post data to true
    CURLOPT_RETURNTRANSFER => TRUE,
    CURLOPT_POSTFIELDS => json_encode($postData),   // post data
    CURLOPT_HTTPHEADER => array("Content-Type: application/json")
  ));

  $response = curl_exec($ch);
  curl_close ($ch);
  $data = json_decode($response, true); // decode the json response
  var_dump($data);
?>
```

> RESPONSE : <code>200</code>

```json
{
  "biofuel_c02_tonnes": 0.011454356557703015,
  "c02_tonnes": 0.0,
  "c02e_tonnes": 1.4155457130358705e-5,
  "ch4_tonnes": 3.2932673188578697e-8,
  "ef_kg_c02e": 0.18456781,
  "n20_tonnes": 4.473872584108805e-8
}
```

Electricity and other sources of energy purchased from your local utility (that is not combusted on-site). Examples include electricity, steam, and chilled or hot water. To generate this energy, utilities combust coal, natural gas, and other fossil fuels, emitting carbon dioxide, methane, and nitrous oxide in the process.

`POST https://dynm-corporate.herokuapp.com/electricity`

<aside>Request params</aside>

| Param                 | Type    | Required | Description                                                       |
| --------------------- | ------- | -------- | ----------------------------------------------------------------- | --- |
| facility_id           | integer | true     | facility id of the company                                        |
| year                  | integer | true     | the year in which the facility wants to calculate ghg emissions   |
| emission_factor_type" | string  | true     | e.g Grid Average/Location Based                                   |
| approach              | string  | true     | e.g Purchased Electricity - Market Based                          |
| amount                | number  | true     | amount of fuel to be consumed                                     |
| units                 | string  | true     | units of the fuel_type to be combusted(e.g., kg or kWh or therms) |     |
| gwp_dataset_revision  | string  | true     |                                                                   |
| scope                 | string  | true     | cross-sectoral emission sources i.e scope 1, 2 and 3              |
| grid_region           | string  | true     | grid region in which the facility is based                        |
| country               | string  | true     | country in which the facility is based                            |

# Refrigerants

> REQUEST

```shell
curl --location --request POST 'https://dynm-corporate.herokuapp.com/refrigerants' \
--header 'Content-Type: application/json' \
--data-raw '{
    "year": 2018,
    "facility_id": 1,
    "refrigerant": "Methane",
    "calculation_method": "Sales Approach (Product)",
    "equipment_type": "",
    "inventory_start": 50,
    "inventory_end": 1,
    "purchased": 0,
    "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
    "scope": "Scope 2"
}'
```

```javascript
const fetch = require("node-fetch");
const data = {
  year: 2018,
  facility_id: 1,
  refrigerant: "Methane",
  calculation_method: "Sales Approach (Product)",
  equipment_type: "",
  inventory_start: 50,
  inventory_end: 1,
  purchased: 0,
  gwp_dataset_revision: "2007 IPCC Fifth Assessment",
  scope: "Scope 2",
};

fetch("https://dynm-corporate.herokuapp.com/refrigerants", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

```python
import requests
import json

url = "https://dynm-corporate.herokuapp.com/refrigerants"

payload = json.dumps({
  "year": 2018,
  "facility_id": 1,
  "refrigerant": "Methane",
  "calculation_method": "Sales Approach (Product)",
  "equipment_type": "",
  "inventory_start": 50,
  "inventory_end": 1,
  "purchased": 0,
  "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
  "scope": "Scope 2"
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
<?php
  $url = "https://dynm-corporate.herokuapp.com/electricity";
  $ch = curl_init($url);
  $postData = array(
    "year"=> 2018,
    "facility_id"=> 1,
    "refrigerant"=> "Methane",
    "calculation_method"=> "Sales Approach (Product)",
    "equipment_type"=> "",
    "inventory_start"=> 50,
    "inventory_end"=> 1,
    "purchased"=> 0,
    "gwp_dataset_revision"=> "2007 IPCC Fifth Assessment",
    "scope"=> "Scope 2"
    );

  curl_setopt_array($ch, array(
    CURLOPT_POST => TRUE, // set post data to true
    CURLOPT_RETURNTRANSFER => TRUE,
    CURLOPT_POSTFIELDS => json_encode($postData),   // post data
    CURLOPT_HTTPHEADER => array("Content-Type: application/json")
  ));

  $response = curl_exec($ch);
  curl_close ($ch);
  $data = json_decode($response, true); // decode the json response
  var_dump($data);
?>
```

> RESPONSE : <code>200</code>

```json
{
  "c02e_tonnes": 1.225
}
```

Includes leaks in your company's HVAC system, chillers, refrigerators, etc., through which refrigerant gas escapes. Most refrigerant gases contribute to global warming when leaked into the atmosphere. The quantity of leaked gas is assumed to equal the amount of gas replaced in these systems by your HVAC or chiller maintenance company.

Records or invoices from your maintenance company show the amount and type of refrigerant gas (e.g., freon, R-22, HFC-134a , CFC-12) replaced in your building's systems.

`POST https://dynm-corporate.herokuapp.com/refrigerants`

<aside>Request params</aside>

| Param                | Type    | Required | Description                                                     |
| -------------------- | ------- | -------- | --------------------------------------------------------------- |
| facility_id          | integer | true     | facility id of the company                                      |
| year                 | integer | true     | the year in which the facility wants to calculate ghg emissions |
| refrigerant          | string  | true     | type of gas used for refrigeration e.g methane                  |
| calculation_method   | string  | true     | method of calculation e.g Sales Approach (Product)              |
| equipment_type       | string  | false    | type of equipment in use                                        |
| inventory_start      | number  | false    |                                                                 |
| inventory_end        | number  | false    |                                                                 |
| purchased            | number  | false    |                                                                 |
| gwp_dataset_revision | string  | true     |                                                                 |
| scope                | string  | true     | cross-sectoral emission sources i.e scope 1, 2 and 3            |

# Results Summary

> REQUEST

```shell
curl --location --request POST 'https://dynm-corporate.herokuapp.com/summary' \
--header 'Content-Type: application/json' \
--data-raw '{
    "stationary_combustion": [{
        "facility_id": 1,
        "year": 2018,
        "fuel_type": "Coal Coke",
        "amount": 1000,
        "units": "kWh",
        "activity_type": "Stationary combustion",
        "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
        "scope": "Scope 1"
    }],
    "mobile_combustion": [{
        "facility_id": 1,
        "year": 2018,
        "fuel_source": "Motor Gasoline",
        "vehicle_type": "Gasoline Passenger Cars",
        "amount": 100,
        "units": "mile",
        "activity_type": "Distance Activity",
        "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
        "scope": "Scope 1"
    }],
    "transportation": [{
        "facility_id": 1,
        "year": 2019,
        "emission_dataset": "US EPA",
        "vehicle_type": "Air Travel - Short Haul (< 300 miles)",
        "mode_of_transport": "Air",
        "category": "Business Travel",
        "amount": 10,
        "units": "mile",
        "activity_type": "Passenger Distance",
        "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
        "scope": "Scope 3"
    }],
    "electricity": [
        {
            "facility_id": 1,
            "year": 2018,
            "emission_factor_type": "Grid Average/Location Based",
            "approach": "Purchased Electricity - Market Based",
            "amount": 100,
            "units": "GJ",
            "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
            "scope": "Scope 2"
        }
    ],
    "refrigerants": [
        {
            "year": 2018,
            "facility_id": 1,
            "refrigerant": "Methane",
            "calculation_method": "Sales Approach (Product)",
            "equipment_type": "",
            "inventory_start": 50,
            "inventory_end": 1,
            "purchased": 0,
            "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
            "scope": "Scope 2"
        }
    ],
    "disaggregation_boundary": "Facility",
    "inventory_data": [
        {"inventory_year": 2018},
        {"inventory_year": 2019},
        {"inventory_year": 2020},
        {"inventory_year": 2021}
    ],
    "facilities": [
        {
        "facility_id": 1,
        "grid_region": "AKGD",
        "country": "USA"
        },
        {
        "facility_id": 2,
        "grid_region": "Ontario",
        "country": "Canada"
        }
    ]
}'
```

```javascript
const fetch = require("node-fetch");
const data = {
  stationary_combustion: [
    {
      facility_id: 1,
      year: 2018,
      fuel_type: "Coal Coke",
      amount: 1000,
      units: "kWh",
      activity_type: "Stationary combustion",
      gwp_dataset_revision: "2014 IPCC Fifth Assessment",
      scope: "Scope 1",
    },
  ],
  mobile_combustion: [
    {
      facility_id: 1,
      year: 2018,
      fuel_source: "Motor Gasoline",
      vehicle_type: "Gasoline Passenger Cars",
      amount: 100,
      units: "mile",
      activity_type: "Distance Activity",
      gwp_dataset_revision: "2014 IPCC Fifth Assessment",
      scope: "Scope 1",
    },
  ],
  transportation: [
    {
      facility_id: 1,
      year: 2019,
      emission_dataset: "US EPA",
      vehicle_type: "Air Travel - Short Haul (< 300 miles)",
      mode_of_transport: "Air",
      category: "Business Travel",
      amount: 10,
      units: "mile",
      activity_type: "Passenger Distance",
      gwp_dataset_revision: "2014 IPCC Fifth Assessment",
      scope: "Scope 3",
    },
  ],
  electricity: [
    {
      facility_id: 1,
      year: 2018,
      emission_factor_type: "Grid Average/Location Based",
      approach: "Purchased Electricity - Market Based",
      amount: 100,
      units: "GJ",
      gwp_dataset_revision: "2007 IPCC Fifth Assessment",
      scope: "Scope 2",
    },
  ],
  refrigerants: [
    {
      year: 2018,
      facility_id: 1,
      refrigerant: "Methane",
      calculation_method: "Sales Approach (Product)",
      equipment_type: "",
      inventory_start: 50,
      inventory_end: 1,
      purchased: 0,
      gwp_dataset_revision: "2007 IPCC Fifth Assessment",
      scope: "Scope 2",
    },
  ],
  disaggregation_boundary: "Facility",
  inventory_data: [
    {
      inventory_year: 2018,
    },
    {
      inventory_year: 2019,
    },
    {
      inventory_year: 2020,
    },
    {
      inventory_year: 2021,
    },
  ],
  facilities: [
    {
      facility_id: 1,
      grid_region: "AKGD",
      country: "USA",
    },
    {
      facility_id: 2,
      grid_region: "Ontario",
      country: "Canada",
    },
  ],
};

fetch("https://dynm-corporate.herokuapp.com/summary", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

```python
import requests
import json

url = "https://dynm-corporate.herokuapp.com/summary"

payload = json.dumps({
  "stationary_combustion": [
    {
      "facility_id": 1,
      "year": 2018,
      "fuel_type": "Coal Coke",
      "amount": 1000,
      "units": "kWh",
      "activity_type": "Stationary combustion",
      "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
      "scope": "Scope 1"
    }
  ],
  "mobile_combustion": [
    {
      "facility_id": 1,
      "year": 2018,
      "fuel_source": "Motor Gasoline",
      "vehicle_type": "Gasoline Passenger Cars",
      "amount": 100,
      "units": "mile",
      "activity_type": "Distance Activity",
      "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
      "scope": "Scope 1"
    }
  ],
  "transportation": [
    {
      "facility_id": 1,
      "year": 2019,
      "emission_dataset": "US EPA",
      "vehicle_type": "Air Travel - Short Haul (< 300 miles)",
      "mode_of_transport": "Air",
      "category": "Business Travel",
      "amount": 10,
      "units": "mile",
      "activity_type": "Passenger Distance",
      "gwp_dataset_revision": "2014 IPCC Fifth Assessment",
      "scope": "Scope 3"
    }
  ],
  "electricity": [
    {
      "facility_id": 1,
      "year": 2018,
      "emission_factor_type": "Grid Average/Location Based",
      "approach": "Purchased Electricity - Market Based",
      "amount": 100,
      "units": "GJ",
      "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
      "scope": "Scope 2"
    }
  ],
  "refrigerants": [
    {
      "year": 2018,
      "facility_id": 1,
      "refrigerant": "Methane",
      "calculation_method": "Sales Approach (Product)",
      "equipment_type": "",
      "inventory_start": 50,
      "inventory_end": 1,
      "purchased": 0,
      "gwp_dataset_revision": "2007 IPCC Fifth Assessment",
      "scope": "Scope 2"
    }
  ],
  "disaggregation_boundary": "Facility",
  "inventory_data": [
    {
      "inventory_year": 2018
    },
    {
      "inventory_year": 2019
    },
    {
      "inventory_year": 2020
    },
    {
      "inventory_year": 2021
    }
  ],
  "facilities": [
    {
      "facility_id": 1,
      "grid_region": "AKGD",
      "country": "USA"
    },
    {
      "facility_id": 2,
      "grid_region": "Ontario",
      "country": "Canada"
    }
  ]
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
<?php
  $url = "https://dynm-corporate.herokuapp.com/summary";
  $ch = curl_init($url);
  $postData = array(
    "stationary_combustion"=> [
        [
            "facility_id"=> 1,
            "year"=> 2018,
            "fuel_type"=> "Coal Coke",
            "amount"=> 1000,
            "units"=> "kWh",
            "activity_type"=> "Stationary combustion",
            "gwp_dataset_revision"=> "2014 IPCC Fifth Assessment",
            "scope"=> "Scope 1"
        ]
    ],
    "mobile_combustion"=> [
        [
            "facility_id"=> 1,
            "year"=> 2018,
            "fuel_source"=> "Motor Gasoline",
            "vehicle_type"=> "Gasoline Passenger Cars",
            "amount"=> 100,
            "units"=> "mile",
            "activity_type"=> "Distance Activity",
            "gwp_dataset_revision"=> "2014 IPCC Fifth Assessment",
            "scope"=> "Scope 1"
        ]
    ],
    "transportation"=> [
        [
            "facility_id"=> 1,
            "year"=> 2019,
            "emission_dataset"=> "US EPA",
            "vehicle_type"=> "Air Travel - Short Haul (< 300 miles)",
            "mode_of_transport"=> "Air",
            "category"=> "Business Travel",
            "amount"=> 10,
            "units"=> "mile",
            "activity_type"=> "Passenger Distance",
            "gwp_dataset_revision"=> "2014 IPCC Fifth Assessment",
            "scope"=> "Scope 3"
        ]
    ],
    "electricity"=> [
        [
            "facility_id"=> 1,
            "year"=> 2018,
            "emission_factor_type"=> "Grid Average/Location Based",
            "approach"=> "Purchased Electricity - Market Based",
            "amount"=> 100,
            "units"=> "GJ",
            "gwp_dataset_revision"=> "2007 IPCC Fifth Assessment",
            "scope"=> "Scope 2"
        ]
    ],
    "refrigerants"=> [
        [
            "year"=> 2018,
            "facility_id"=> 1,
            "refrigerant"=> "Methane",
            "calculation_method"=> "Sales Approach (Product)",
            "equipment_type"=> "",
            "inventory_start"=> 50,
            "inventory_end"=> 1,
            "purchased"=> 0,
            "gwp_dataset_revision"=> "2007 IPCC Fifth Assessment",
            "scope"=> "Scope 2"
        ]

    ],
    "disaggregation_boundary"=> "Facility",
    "inventory_data"=> [
        [
            "inventory_year"=> 2018
        ],
        [
            "inventory_year"=> 2019
        ],
        [
            "inventory_year"=> 2020
        ],
        [
            "inventory_year"=> 2021
        ]
    ],
    "facilities"=> [
        [
            "facility_id"=> 1,
            "grid_region"=> "AKGD",
            "country"=> "USA"
        ],
        [
            "facility_id"=> 2,
            "grid_region"=> "Ontario",
            "country"=> "Canada"
        ]
    ]
 );

  curl_setopt_array($ch, array(
    CURLOPT_POST => TRUE, // set post data to true
    CURLOPT_RETURNTRANSFER => TRUE,
    CURLOPT_POSTFIELDS => json_encode($postData),   // post data
    CURLOPT_HTTPHEADER => array("Content-Type: application/json")
  ));

  $response = curl_exec($ch);
  curl_close ($ch);
  $data = json_decode($response, true); // decode the json response
  var_dump($data);
?>
```

> RESPONSE : <code>200</code>

```json
{
  "disaggregation": {
    "1": {
      "Scope 1": {
        "Mobile Combustion": {
          "2018": 0.0,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        },
        "Refrigerants/Fugitive Emissions": {
          "2018": 1.225,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        },
        "Stationary Combustion": {
          "2018": 0.390355827342494,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        }
      },
      "Scope 1(Biogenic)": {
        "2018": 0.0,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Scope 2": {
        "Heat/Steam": {
          "2018": 0.0,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        },
        "Purchased Electricity - Location Based": {
          "2018": 0.0,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        },
        "Purchased Electricity - Market Based": {
          "2018": 13.16631238777778,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        }
      }
    },
    "2": {
      "Scope 1": {
        "Mobile Combustion": {
          "2018": 0.0,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        },
        "Refrigerants/Fugitive Emissions": {
          "2018": 1.225,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        },
        "Stationary Combustion": {
          "2018": 0.390355827342494,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        }
      },
      "Scope 1(Biogenic)": {
        "2018": 0.0,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Scope 2": {
        "Heat/Steam": {
          "2018": 0.0,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        },
        "Purchased Electricity - Location Based": {
          "2018": 0.0,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        },
        "Purchased Electricity - Market Based": {
          "2018": 13.16631238777778,
          "2019": 0.0,
          "2020": 0.0,
          "2021": 0.0
        }
      }
    }
  },
  "results": {
    "Scope 1": {
      "Fugitive emissions from air-conditioning": {
        "2018": 1.225,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Mobile Combustion": {
        "2018": 0.039,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Stationary Combustion": {
        "2018": 0.390355827342494,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "total": {
        "2018": 1.654355827342494,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      }
    },
    "Scope 1(Biogenic)": {
      "2018": 0.0,
      "2019": 0.0,
      "2020": 0.0,
      "2021": 0.0
    },
    "Scope 2": {
      "Heat/Steam": {
        "2018": 0.0,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Purchased Electricity - Location Based": {
        "2018": 0.0,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Purchased Electricity - Market Based": {
        "2018": 13.16631238777778,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Scope 2 - Location based + Heat/Steam": {
        "2018": 13.16631238777778,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Scope 2 - Market based + Heat/Steam": {
        "2018": 0.0,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      }
    },
    "Scope 2(Biogenic)": {
      "2018": 0.0,
      "2019": 0.0,
      "2020": 0.0,
      "2021": 0.0
    },
    "Scope 3": {
      "Business Travel": {
        "2018": 0.0,
        "2019": 0.00227010675965,
        "2020": 0.0,
        "2021": 0.0
      },
      "Employee Commute": {
        "2018": 0.0,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      },
      "Upstream T&D": {
        "2018": 0.0,
        "2019": 0.0,
        "2020": 0.0,
        "2021": 0.0
      }
    },
    "Scope 3(Biogenic)": {
      "2018": 0.0,
      "2019": 0.0,
      "2020": 0.0,
      "2021": 0.0
    }
  }
}
```

GHG Emissions Summary

`POST https://dynm-corporate.herokuapp.com/summary`

<aside>Request params</aside>

| Param                        | Type    | Required | Description                                               |
| ---------------------------- | ------- | -------- | --------------------------------------------------------- |
| facility_id                  | integer | true     | facility id of the company                                |
| stationary_combustion params |         | true     | request parameters required for stationary combustion     |
| mobile_combustion params     |         | true     | request parameters required for mobile combustion         |
| electricity params           |         | true     | request parameters required for purchase electricity      |
| refrigerants params          |         | true     | request parameters required for refrigerants calculations |
| inventory_data               |         | true     | inventory years keyed in to calculate the summarry        |

# Fuel Types

<aside>Fuel Types</aside>

| Fuel Type                   | Fuel Type                | Fuel Type                |
| --------------------------- | ------------------------ | ------------------------ |
| agricultural byproducts     | distillate fuel oil no 1 | petrochemical feedstocks |
| peat                        | distillate fuel oil no 2 | petroleum coke           |
| solid byproducts            | distillate fuel oil no 4 | propane                  |
| wood and wood residuals     | ethane                   | propylne                 |
| natural gas                 | ethylene                 | residual fuel oil no 5   |
| blast furnace gas           | heavy gas oils           | residual fuel oil no 6   |
| coke oven gas               | isobutane                | special naphtha          |
| fuel gas                    | isobutylene              | still gas                |
| propane gas                 | kerosene                 | unfished oils            |
| landfill gas                | kerosene type jet fuel   | used oils                |
| other biomass gases         | liquefied petroleum gas  | biodiesel 100 percent    |
| compressed natural gas      | lubricants               | ethanol 100 percent      |
| asphalt and road oil        | motor gasoline           | rendered animal fat      |
| aviation gasoline           | naphtha 401 deg f        | diesel fuel              |
| butane                      | natural gasoline         | liquefied natural gas    |
| butylene                    | other oil 401 def f      | methanol                 |
| crude oil                   | pentanes plus            | residual fuel oil        |
| anthracite coal             | vegetable oil            | bituminous coal          |
| sub bituminous coal         | lignite coal             | mixed commercial sector  |
| mixed electric power sector | mixed industrial cooking | coal coke                |
| municipal solid waste       | petroleum coke solid     | plastics                 |
| plastics quad short ton     | tires                    |                          |
