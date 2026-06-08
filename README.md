# Tableau-vs-Power-BI
1) Datasources options are more in Tableau
2) Types of visualizations are more in Power Bi
3) Data cleaning needs separate software for Tableau but it is built in for Power Bi
4) Publishing time we can select the dashboards for Tableau but Power bi requires individual hide
5) Power Bi has more built in option to download/share as excel
   --Self Learning by converting
   1) Adjust the canvas size: Paint icon at the right is for formatting > Canvas Setting > Custom > 900 height, 1600 width
   2) Tableau: Tiled / Floating, Power BI: Only Floating
   3) Tableau: Title, Power BI: Use Text Box
   4) Score Card: You can add multiple scores in one card. Format > Visual > Callout > Value/Label (for multi Card formatting title and value)
                                                            Format > General > Data Format > Value/Label
   5) If Display Units are not visible, you can add FORMAT(value,"0") in calculation. It works for Score card but wasn't able to add to X axis of bar graph. Then I created new calculation without using FORMAT.
   6) If format Date doen't work create a new column with the necessary format. To sort this column on a visual add the original date field to tooltip. Then click on the 3 dots at the top right of the visual and sort based on this original date field.
   7) Had to create a new column for class decades (e.g.: 1980-1990 is Class of 80's) as creating new measure didn't work
   8) By default action filter is active with all visualizations and we have to disable that if we don't want
   9) Manual Sorting is not available: Instead create a duplicate metric column and sort order column dax saying which metric is 1,2,3 etc. Then sort the duplicate metric legend with the sort order column
   10) Tooltip - Tableau has more options
   11) If we have to show multiple measures in a sheet as a bar graph and sort, we have either unpivot (if the fields are columns) or create a new table with measure names and write a switch calculation for measure selection in the original table.
   12) Equivalent of IFNULL in Tableau is COALESCE in Power BI
   13) Page Title is through text box, insert shape(rectangle) or card
   14) click here to details navigation
       a) Button Navigation: Insert → Buttons → Blank, Format>Text = On, Action = On, Type = Page navigation>Destination = Select your detail page
       b) Text Box as Link
       c) Dynamic drill-through navigation (using drill-through filters)
   15) In Tableau, when you create a calculated field it becomes either a dimension or a measure. But in Power BI, we have to identify that first and create new column in the data model or create new measure(just like calculated field in Tableau)
   16) | Tableau                      | Power BI Equivalent                            |
| ---------------------------- | ---------------------------------------------- |
| Relationship (logical layer) | Relationship                                   |
| Join (physical layer)        | Merge in Power Query / SQL join before loading |

# Main tradeoff

| Relationships             | Merge Queries (through Power Query)           |
| ------------------------- | ------------------------ |
| Tables stay separate      | Tables become one        |
| Better for scalable BI    | Better for preprocessing |
| Smaller model             | Larger model             |
| Dynamic filtering         | Static flattened data    |
| Preferred for star schema | Useful for enrichment    |
For relationship, you need to set cardinality and cross-filter direction (single or both)

# Easy rule
### If you’re thinking:> “I need this table to filter another table”
→ use **relationship**

### If you’re thinking:> “I need these columns physically inside the same table”
→ use **merge query**

17) Creating Date Parameter: You have to create date tables either using calendar function or using existing dim_date
    - Create one date parameter, change the properties to between. Adjust the calculation of Total Tickets to choose from the min and max value of the date parameter.
    - Total Tickets = 
      VAR StartDate =
          MINX(
              ALLSELECTED('Start Date Parameter'),
              'Start Date Parameter'[Date]
          )
      
      VAR EndDate =
          MAXX(
              ALLSELECTED('Start Date Parameter'),
              'Start Date Parameter'[Date]
          )
      
      RETURN
      CALCULATE(
          DISTINCTCOUNT(ticket[obj_oid]),
          ticket[close_date] >= StartDate,
          ticket[close_date] <= EndDate
      )<img width="717" height="292" alt="image" src="https://github.com/user-attachments/assets/d82770a0-d109-46ba-8dba-b4d07bb8173a" />

    18)  | Tableau | Purpose                   | Power BI Equivalent       |
         | ------- | ------------------------- | ------------------------- |
         | FIXED   | Ignore visual granularity | `CALCULATE` + `ALLEXCEPT` |
         | INCLUDE | Add lower granularity     | `SUMX` + `VALUES`         |
         | EXCLUDE | Remove one dimension      | `ALL` / `REMOVEFILTERS`   |

    19)  | Tableau                  | Power BI Equivalent                  | Notes                             |
         | ------------------------ | ------------------------------------ | --------------------------------- |
         | Extract Filter           | Power Query filter / Dataflow filter | Applied during data load          |
         | Data Source Filter       | Model-level filter / Power Query     | Restricts data for entire dataset |
         | Context Filter           | DAX filter context                   | No direct “context filter button” |
         | Dimension Filter         | Visual/Page/Report filter            | Most common filters               |
         | Measure Filter           | Visual-level measure filter          | Similar behavior                  |
         | Table Calculation Filter | Visual interaction / DAX             | Different implementation          |

    20) { FIXED [Ticket Id] : MAX([Repair Price]) }
        Total Repair Price =
         SUMX(
             VALUES(ticket[obj_oid]),
             CALCULATE(
                 MAX(ticket[Repair Price])
             )
         )




