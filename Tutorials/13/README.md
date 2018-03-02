# Your Thirteenth M# Application
In this tutorial you will learn:

- Control type
- Form element data source
- Form element Source criteria

## Requirements
In this tutorial we are going to implement a web site that manages countries and resellers. Countries can be from European or not, but resellers can be just from European countries. By clicking on each country use can see its related cities and customers.

### Countries:
![Countries](Countries.PNG "Countries")

![City Add/Edit](CityAdd.PNG "City Add/Edit")
In country page user can see a list of all countries and he can do CRUD operations. The user is also able to click on each country and see its detail like below:

![Country View](CountryView.PNG "Country View")

![City Add/Edit](CityAdd.PNG "City Add/Edit")

![Customer Add/Edit](CustomerAdd.PNG "Customer Add/Edit")

In country detail page user can see all related cities and customers and is able to do CRUD operations. There are some criteria for concern:
- Only cities that are linked to the CURRENTLY selected Country should be listed here, instead of All cities.
- Only customers that are linked to the CURRENTLY selected Country should be listed here, instead of All customers.
According to the requirements, we should just load selected country's cities and customers.

### Resellers:
![Resellers](Resellers.PNG "Resellers")

![Reseller Add/Edit](ResellerAdd.PNG "Reseller Add/Edit")

In reseller page user can see all resellers and he is able to do CRUD operations. For adding new reseller there is a criteria for concern:
- Only European countries should be listed.

## Implementation
From requirements, four entities can be identified, "Country", "Reseller", "City" and "Customer". Country entity has many cities, customers and resellers. Reseller entity has one country. City entity has one country. Customer has one reseller and one country.
After understanding requirements and identifying its related properties, it's time to create them. Now let's create the corresponding classes in the *#Model* project.

[Comming soon]