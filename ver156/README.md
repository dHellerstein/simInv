# simInv

This is version 1.56. As of April 2024, the latest version 1.80. We recommend using the latest version.

simInv: simulate the performance of one or more investment portfolios
 
  simInv allows you to compare the performance of alternative investment portfolios.
  simInv tracks & displays the gross and net (after-tax and after inflation ) value of a portfolio -- a mix of assets --  over time.

Several kinds of assets can be specified: bonds, stocks, properties, and incomeStreams.

  An investment portfolio contains a  set (a mix) of assets.  Different investment portfolios can contain different mixes of assets.
  Each portfolio can be modified -- changing which assets it contains (or changing quantities of existing assets) .
  You can modify a portfolio as often as your want. You specify the date of a modification, and its new asset mix.


## In short:
        *  Portfolios grow over time -- bonds growing at an interest rate, and dividends used to purchase more of a stock, and income accumulating.
            Or it could shrink, if expenses are greater than earnings!

        *  Portfolios are dynamic -- the mix of assets they contain can be modified over time.

        *  The value of each asset can change over time -- such  as the price of a stock or a property, or the interest earnings of bond.
           These changes have nothing to do with your portfolios -- they reflect what's happening in the "real world".

        *  Thus: on a given date, the value of a portfolio depends both on its asset mix  and the price, etc. of assets on that date.

##  And the point is ...

     *  Portfolios are independent --  you are NOT dividing a set quantity of money across portfolios.

	Instead: you are comparing what happens to a starting investment.
        Thus: when comparing portfolios, it is useful to create them wth the same starting investment (the same amount invested in their asset mix).

      * When modfications are specified: simInv checks for feasibility -- are the funds available (in a portfolio on a given date) able to
        acquire the desired asset mix?  And that includes accounting for tax payments if assets are sold.

      *  simInv encourages honest comparisons across portfolios!
         That means that the asset histories should reflect reality; with accurate updates as time goes by.


## See `readme.txt` 
_for more details_ on how to use simInv, and for the GNU 3.0 disclaimer

# Installation:

simInv is distributed in a simInv_xxxx.zip file.
It should be unzipped to an empty directory.  

simInv can be run in two modes:

+ _online mode_ --  requires a server that supports php 7.0 or above.
       simInv should be unzipped to a web accessible directory
     
+  _standalone_ mode ** -- can be run directly from a browser accessing a file on your computer
       simInv can be unzipped to any directory on your computer 

See `install.txt` for installation details

