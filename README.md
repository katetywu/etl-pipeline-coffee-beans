## ETL Pipeline - Green Coffee Beans Scrape

### Contributors
* [Mahlon Duke](https://github.com/mahlonduke)
* [Kate Wu](https://github.com/katetywu)

### Abstact
Save independent coffee roasters time and money by providing them with a single interface for searching multiple marketplaces for the best green coffee beans at the best price.

### Introduction
The industry of coffee roasting is dominated by a small group of large companies, such as Starbucks and Yuban.  To target a wider audience, these companies typically create coffee roasts which are approachable to most potential customers from a price and flavor complexity standpoint.  However, this aim at wider audiences means that these coffees often don’t satisfy the more refined coffee consumer.  These customers instead turn to smaller, local coffee roasters which, as small businesses, operate on much slimmer margins.  That means that any extra time which the roaster spends on business management tasks like finding a good green coffee bean at a good price is less time spent crafting newer and better roasts to further promote their business, and might lose further money by purchasing beans at a higher price than they could otherwise be obtained for.

### Methodology
Because there is no single service which combines green coffee bean marketplaces into one portal, data on bean prices and ratings must be pulled from multiple disparate websites.  These websites are often smaller, and therefore don’t offer a dedicated API for obtaining this information.  To obtain the data, we need to scrape the websites themselves.

#### Dataset
* [Amazon](https://www.amazon.com/Best-Sellers-Grocery-Gourmet-Food-Unroasted-Coffee-Beans/zgbs/grocery/979887011)
* [Coffee Bean Corral](https://www.coffeebeancorral.com/categories/Green-Coffee-Beans/All-Coffees.aspx)
* [Deans Beans](https://deansbeans.com/our-products/roasted-coffees/green-unroasted-coffee-beans.html)
* [Fresh Roast Coffee](https://www.freshroastedcoffee.com/collections/green-coffee)

#### Variables
Each variable was scraped from each website using the Splinter web scraper, initiated from within a Jupyter Notebook running Pandas.
* Name: name of  the bean, which includes key details like the region the bean was grown in
* Price: price of the bean
* Rating: rating of the bean (1-5 scale)
* URL: link of the individual listing for each bean
* Source: online retailer of the bean

#### Cleaning Process
Once the data had been scraped, it was then combined into a new dataframe. Separate dataframes were created for each website source, so that the data could be cleaned according to that website’s unique style of presenting data.
* Removing the dollar sign from the price, so that the data can be treated as a number for filtering and sorting purposes.  “$1.23” to “1.23”.
* Removing extraneous words from the rating, so that just the score is retained.  “4.2 out of 5 stars” to “4.2”

#### Uploading
The cleaned dataset was then pushed into a SQL database, hosted on the local machine, as a single table containing all of the pertinent bean information.