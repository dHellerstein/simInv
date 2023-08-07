# simInv
simInv: simulate the performance of one or more investment portfolios

6 August 2023. simInv 1.5 -- simulate the peformance of investment portfolios.


1.  What is simInv
2. Details on the types of assets
3. Installation
3a.  Installing in online mode.
3b.  Installing in standAlone mode.
3c.  Removing users
3d. Switching storage modes
4.  Using simInv  .
5. Limitations
6. Disclaimer

                      ----------------------------------- 

1. What is simInv?

  simInv allows you to compare the performance of alternative investment portfolios.
  simInv tracks & displays the gross and net (after-tax and after inflation ) value of a portfolio -- a mix of assets --  over time.

 Several kinds of assets can be specified: bonds, stocks, properties, and incomeStreams.

  An investment portfolio contains a  set (a mix) of assets.  Different investment portfolios can contain different mixes of assets.
  Each portfolio can be modified -- changing which assets it contains (or changing quantities of existing assets) .
  You can modify a portfolio as often as your want. You specify the date of a modification, and its new asset mix.

    For each asset a "history" is specified -- that describes the trend (over time) of the price, interest, or dividend rate of the asset.
       *  On any given date: linear interpolation is used to calculate an asset's price, interest, or dividend -- using the nearest (in time)
          "history" entries.
          Thus: for stable assets, an asset history does not need many entries.

   An asset's history is the same regardless of what portfolio(s) the asset may be part of.

   In short:
        *  Portfolios grow over time -- bonds growing at an interest rate, and dividends used to purchase more of a stock, and income accumulating.
            Or it could shrink, if expenses are greater than earnings!

        *  Portfolios are dynamic -- the mix of assets they contain can be modified over time.

        *  The value of each asset can change over time -- such  as the price of a stock or a property, or the interest earnings of bond.
           These changes have nothing to do with your portfolios -- they reflect what's happening in the "real world".

        *  Thus: on a given date, the value of a portfolio depends both on its asset mix  and the price, etc. of assets on that date.

  And the point is ...

     *  Portfolios are independent --  you are NOT dividing a set quantity of money across portfolios.

	Instead: you are comparing what happens to a starting investment.
        Thus: when comparing portfolios, it is useful to create them wth the same starting investment (the same amount invested in their asset mix).

      * When modfications are specified: simInv checks for feasibility -- are the funds available (in a portfolio on a given date) able to
        acquire the desired asset mix?  And that includes accounting for tax payments if assets are sold.

      *  simInv encourages honest comparisons across portfolios!
         That means that the asset histories should reflect reality; with accurate updates as time goes by.

The following briefly describes simInv.  simInv has extensive on line help -- read it for the details!

2. Details on the types of assets:

    * "bonds" : an asset that grows at an interest rate.   For example: a savings account, a CD, or bond fund.  Interest earnings are taxable.
      A tax-free fraction of interest earnings can be specified. For example, 1.0 for a municipal bond fund that is not subject to taxes.
      Or, a Roth IRA (with 1.0 tax free fraction).

      Unless you specifically "sell" bonds (in a portfolio modification:
          The interest earnings of a bond asset are always retained -- 
          so the bond's value grows over time at the rate of after-tax-interest.

      You can specify "yearly" additions to a bond fund -- which come out of `Cash`.

    * "tax deferred bond" :  a bond whose earnings are tax deferred. Taxes are paid only when the "bond" is sold -- and the taxes
      are on the sale price of the bond (not just on its interest earnings). For example: an IRA or a 401k

      The interest earnings of a tax deferred bond are always retained -- so the bond's value grows over time at the rate of interest.

      You can specify "yearly" additions to a tax-deferred bond fund -- which come out of `Cash`.
      
      In addition to assets whose history you explicitily specify, simInv comes with a number of "public assets" -- stocks and funds available
      on the market.
      Users can add these assets to the list of "available assets" (assets that can be   added to a portfolio) as needed.

   *  "stocks" : an asset that yields a dividend and whose price can change.  Dividends are taxable, as are capital gains when a stock is sold.
      For example: a publically traded stock.

      The divdend earnings of a stock are always used to purchase more of the same stock - so the # of shares increases over time .
      The rate of increase is a function of dividend/price -- since both can fluctuate, so can this rate of incrase!

   * properties: an asset that has a price, and  Rent, that can change.

     Rent is yearly income from a property -- such as   rental income minus property taxes.  If income is low and expenses are high, the Rent can be negative!
     Properties can be purchased with loans -- you specify the terms of the loan when you add a property asset.
         Rents, and sales of properties,  are  saved to `Cash` .
         Loan payments are withdrawn from `Cash`.
         You can refinance loans.

     In particular:
       *  Rents  (positive or negative) due to a property are  NOT reinvested in the property.
       *  The "value" is  obtained when the property is sold in its entirety -- after paying off remaining loan balance and capital gains taxes.
       *  Fractional pieces of a property can not be sold.

     When sold, properties are subject to capital gains tax -- whose rate can be specified.
        For example: a vacation home  may be treated as a personal property when sold
        (hence not subject to full capital gains tax).

   * incomeStreams:  a yearly income (or a debit, if negative).

      The income is taxed, and the resulting revenue is added to the `Cash` asset.
      incomeStreams have no "sale" value -- when they end, the income they yields stops (with no other impact).
      You can specify negative incomeSteams -- for example, a yearly obligation, or living expenses.

      There are two types of income streams:
         * varying over time (as specified in its asset history), and
         * fixed when acquired.  The income flow is fixed once the asset is acquired (using a value derived from the asset history).
          It isn't strictly fixed -- it can grow at a fraction of the inflation rate.

      Examples:
        *  social security payments are fixed -- depending on the age you enroll. But they do grow over time
        *  a part time job can be varying -- the income recieved can go up or down.
        *  expenses (such as yearly charitable donations) are specified as negative values. They can be fixed or varying.

 * `Cash` : this is where non-allocated portion of your budget, and  positive revenues (income and netRent) are placed.
      It is also where over-allocations,  debts (such as negative  Rents), and loan payments are extracted from.

      This is NOT directly modified -- it is auto-calculated based on the performance of your asset-mix.

     `Cash` is  subject to two interest rates : one when `Cash` is greater than 0, and another when it is less than 0.
      For example: a very low rate for positive `Cash` balances (for example, 0.1% in a savings account:
                   a high rate for negative `Cash` balances (for example, 11.5% for a credit card).

     Assuming the above:
         it is best  to have enough `Cash` to cover expenses (such as loan payments), but not much more (or less).
     That means it is useful to modify your portfolio regularly -- selling or purchasing assets as your `Cash` balance changes

3. Installation:

  simInv can be run in two modes:

    * online mode --  requires a server that supports php 7.0 or above.
    * in standalone mode -- can be run directly from a browser accessing a file on your computer

   Advantages and disadvantages

      Online mode
       * Accessible from anywhere via the web
       * Requries installation on a http: (or https:) server that
            i) supports php 7.0 or above
           ii) allows php to write files to a directory
       * Users do not have to worry about file maintenance
       * Security is not great -- though encryption can help.
       * publicAssets can be modified.

     Stand alone applicaton
       * Accessible from a user's computer -- a file:// url can be used
       * Does NOT require a server -- and does not require php
       * Uses local file storage. Some browser installations may not enable local file storage
       * Users are responsible for maintaining files. In particular: archiving local file storage files requires a few steps.
       * Fairly secure, so long as users control access to their computer
       * Anyone with access to this computer can view all of the simInv users (who are using the same computer)
       * public assets can not be modified. 


3a.  Installing in online mode.

    The simInv administrator should

      a) Create a simInv directory in a web accessible directory
      b) Unzip simInv_vxxx.zip to this directory.

      Several subdirectories are created: lib/, publicAssets/,  and data/.
          An  archive/ directory is also created -- but is not directly used by simInv. 
          It's a convenient place to place archive files (when   running in standAlone mode)

    c)     The data/ directory will contain subdirectories for each user.

        ***   It is the administrators job to create directories for each recognized user.  ***

       For example: for user "joeb" the admin should create data/joeb

       Note: simInv comes with a "test" user specified. You can use it for testing and demo purposes!

    d)  Load simInv.php with your favorite javascript capable browser.
        For example: http://mysite.org/simInv/index.html

   e) Note that the 'useLocalStorage' variable (in index.html) should equal 0 

  Users should logon with one of the usernames created in step (c).


3b. Installing in standAlone mode

 There are two variants of 'standAlone' mode:  'noWeb'  and 'www'. Both use local storage of data.

  * 'noWeb'  -- simInv is loaded locally
      Users must download the simInv package, but do not need future access to the web!

    a) The user should unzip simInv_vxxx.zip to an empty directory.
       For example: d:/myStuff/simInv
       Note that the data/, publicAssets/, and lib/  directories are created, but data/ is not used in standAlone mode.
       The user could use it to archive his simInv data!

    b) In your browser, enter a file:// url to index.html.
         For example: file:///d:/myStuff/simInv/index.html

    c) Enter a username. The first time, simInv will initialize simInv data for this data -- using local storage.
      The user can use as many usernames as desired -- each user data is stored seperately

  * 'www' access -- simInv is loaded via the web (i.e.; using http://mysite.org/simInv/)

      Users do NOT have to download the simInv package, but need accesss to the web to load it in the future!

    a)  As with 'onLine' mode, the simInv administrator should unzip simInv_vxxx.zip to a web accessible director on a http (or https)   server.

    b)  Using a text editor, edit index.html  (in the directory where simInv was installed), and set the "global variable":
           useLocalStorage=1
       This should be around line 10.

  As with online mode, users can then load index.html from the web.
  However: as with 'local' mode -- all data for each user will be stored on the user`s own computer. 
  Thus, the admin does NOT need to create directories under data/

  Notes:

    * local data storage depends on how you access simInv.

      In particular: accessing simInv using a file:/// url or via the web (with useLocalStorage=1) uses seperate data files.
      For example: user data when accessing index.html via  file:///pathToSimInv/index.html will NOT be available when accessing index.html via the web.

    * you can use archive and restore to move a user`s simInv data across modes.
    
    * some browsers do not support local storage.

3c.  Removing users, and clearing data

To remove a user ..

 *  onLine mode -- requires access to simInv directory on the server

       i) In simInv/data : find the subdirectory for the use
     ii) Erase all its files!
        The next time the user logs in, she will be asked to initialize.
    iii) Or, remove the directory -- the user will not be allowed to login

 *  onLine mode -- anyone with access to the computer (that simInv is using for local storage) 
       i ) logon as the desired user
      i i) Click diskette icon (in the upper right corner)
     iii) Click the 'remove this user' button on the page that appears
                                                       
     Hint: you can switch to another user (on this computer) using the list of users (at the bottom of this page).
     That means: anyone with access to this computer can see data for all users.


3d. Switching storage modes         

   simInv can give users the choice between online and standalone modes.  
   The user chooses which mode when she first logons -- and this mode is used for all future logons. By all simInv users using this computer.

  To enable this, in simInv/index.html set the following variables (around line 10)
      var useLocalStorage=0         ;
      var useLocalStorageChoice=1 ; 

  Note that in local storage mode (useLocalStorage=1) -- the user does NOT have a choice of storage modes.

 On the first logon to simInv, a menu will ask what mode to use. And this mode will be used for all future logons.
  For all users who are working with this computer!

Changing storage modes

   You can use clearLocalStorage.html to change storage modes. Or you can work with browser settings.

   * clearLocalStorage.html (in main simInv/ directory)
     Your current local storage (if any) is displayed, and you can change it.
     However, as a security measure the capability of changing modes is disabled.

     To enable -- set the following variable in clearLocalStorage.html  (near line 10):

         allowChanges=1

   Or, if you are comfy working with your browser's settings ....

         Find the local storage menu for your browser  and change the simInv_!useLocal variable

	 Example: for Firefox
	    i) Logon to simInv in your normal fashion
                    ii) Hit the F12 key (or RMB on the page and select `Inspect (Q)`)
                   iii) Click the `storage` choice on the button bar
                    iv) Click on `Local Storage`
                     v) Click on the site
                    vi) In the Key column, find `simInv_!useLocal`
                   vii) Delete that row

          Logon to simInv -- you will be asked to select a storage mode!

    Reminder: choice of storage mode is  NOT enabled if standAlone mode is used --
              if useLocalStorage=1 or if a file:/// url is used to access simInv

   Hints:
     *  archive user data beforehand, so you can restore them (after changing the storage mode).
     *  clearLocalStorage.html displays local storage information, and provides further details

4.  Using simInv  .....

   While not required, each user may want to change the personal settings when they first logon.
   The first time a user logons on, a few initialization steps are taken. The steps depend on whether onLine or standAlone mode is used.

   In either case: ater succesfully logging and initializing, a user may want to change his personal settings.

   User should then create their own assets and portfolios.
   This can be done at any time -- with new assets and new portfolio mixes added as convenient.
   But use some caution: specifying a modification with a date that is in between existing modifications can have odd effects on porfolio specification.
   Similarly, revising  an asset history  -- adding entries that occur before the specified date of an  existing modification -- can have odd effects.

   The online help outlines how to work with asset and portfolios.

  Note that users can add "publicAssets" -- assets whose attribute and history come with simInv's distribution.
  See publicvAssets/readme.txt for instructions on how to add publicAssets!

Limitations:

   simInv has a relatively simple inflation model -- using a yearly CPI series for all values (that can be modified as needed).

   It is recommended that all values (such as  prices, etc in the asset historys) be entered as actual values (not inflation adjusted).

   simInv has a fairly simple algorithim for accounting for taxes.
        Taxes on earnings (interest from bonds, dividends from stocks) are collected on a "daily" basis.
        Taxes on sales (of stocks) and withdrawals of tax-deferred bonds are collected when they occur (on modification dates).

        Negative capital gains can offset  positive capital gains (to reduce capital gains tax), but can not be transferred to other sources of income.
        Capital gains occur when properties and stocks are sold -- the sum of all these sales (minus their basis) is used to compute a capital gains tax.

      The total revenue (across all incomeStreams and netRents) is used to calculate taxes.
               Losses from incomeStreams, and netRents, can be used to reduce the taxable total revenue.
               This means your "daily" tax bill is reduced, with positive impacts on `Cash`.

      Changes in tax-deferred bonds can offset (so moving from one tax-deferred bond to another will not require paying a tax).
      But a modification that leads to a net decrease in the aggregate value of a portfolio's tax-deferred bonds will be taxed (even if the next
      day this decrease is reallocated to a tax-deferred bond).

   simInv, when run in onLine mode, is not very secure
       However, simInv can encrypt all data saved on the server -- which requires that the user specify, and remember, an encryption key.

      In standAlone mode simInv should be quite secure -- assuming you control access to your computer.
      As of 3 August 2023, standAlone mode does NOT encrypt data.

   simInv uses some approximations to calculate revenues, taxes, and growth. These can be less accurate if time spans between modifications are large
   (say, several years long).

Contact: Daniel Hellerstein. danielh@crosslink.net.
       http://www.wsurvey.org/distrib, or  https://github.com/dHellerstein

6. Disclaimer:

    simInv is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    simInv is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    If you did not receive a copy of the GNU General Public License,
    see <http://www.gnu.org/licenses/>.

    Note: simInv uses security measures that are not strong.
          In particular: if you do not control access to the directory that simInv
                         (index.html, simInv2.php, and other files) is installed on  ...
                     --  you should NOT install simInv on your web server, or on your personal computer!


