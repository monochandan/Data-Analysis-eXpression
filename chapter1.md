Sum of all sales amount
        
    AllSales := SUM(Sales[SalesAmount])


Compute the sum of all sales using the SUMX iterator:

    Allsales := SUMX(Sales, Sales[ProductQuantity] * Sales[ProductPrice]) 

DAX expressions are by default LEFT OUTER JOIN. 
Customer name with total amount of money they have expended on products :

    EVALUATE
    SUMMARIZECOLUMNS ( 
        Customers[CustomerName], ## ---- group by this column using the function summarizecolumns
        "SumOfSales", SUM(Sales[SalesAmount]) ### --- new column sumofsales after the aggregation function SUM on salesammount
    )

Customer who lives in EUROPE only:
Used FILTER :

         EVALUATE
        SUMMARIZECOLUMNS ( 
        Customers[CustomerName], 
        FILTER (
                Customers,
                Customers[Continent] = "Europe"
        )
        "SumOfSales", SUM(Sales[SalesAmount])
        )

Customers who baught more than 100 dollar:

         EVALUATE
        FILTER ( 
        SUMMARIZECOLUMNS (
                Customers[CustomerName], 
                "SumOfSales", SUM(Sales[SalesAmount])       
        ),
        [SumOfSales] > 100
        )
