#Adding Formatting Options to Izenda Reports Formatting to Grid or New Formats to Formats Dropdown

[[_TOC_]]

##About

Here we will show you how to easily add a new formatting option to the "Formats" dropdown menu on the Fields tab of the Report Designer. These should be handled in your ``InitializeReporting()`` method in your global.asax.

##Method 1

In this example, we will quickly add a new format option to the list called "Bold". New formats added this way will be available for every type of data and will not override the existing built-in formats for each type of data. The symbol {0} acts as a token to represent the data that is returned by the query.

```csharp
    AdHocSettings.Formats.Add("Bold", "<strong>{0}</strong>");
```

##Method 2

We can also use an Izenda Format object as an argument. Below is the method of adding a formatting option called "Scientific" to the list of formats. Items added this way can be made available for specific **SqlTypeGroups** and will not override any of the existing formats.

```csharp
    SimpleFormat scientificFormat = new SimpleFormat("Scientific", "{0:E}", new SqlTypeGroup[] {SqlTypeGroup.Real, SqlTypeGroup.Numeric});
    AdHocSettings.Formats.Add("Scientific", scientificFormat);
```

##Results

Below are screenshots of the results. The one directly below this text shows the OrderID field (a number field) with both of our new functions listed.

![Extended Formats](/FAQ/Questions/Add-Formatting-Options/extended_formats.png)

And here is the Freight field formatting options. Notice that we did not specify the "Money" type in our **SqlTypeGroups** for the Scientific format. Therefore, it is not listed in this dropdown but "Bold" still is.

![Extended Formats 2](/FAQ/Questions/Add-Formatting-Options/extended_formats_2.png)