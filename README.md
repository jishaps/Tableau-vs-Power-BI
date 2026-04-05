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
