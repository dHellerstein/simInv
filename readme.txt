14 April 2024. simInv 1.8 -- simulate the peformance of investment portfolios.


1. What is simInv
2. Details on the types of assets
3. Installation
3a.  Installing in online mode.
3b.  Installing in standAlone mode.
3c.  Removing users
3d.  Switching storage modes
3e.  Clearing local storage
3f.  Updating schedules
3g.  Updating public assets
4. Using simInv
5. Limitations
6. Disclaimer

                      -----------------------------------

1. What is simInv?

  simInv allows you to compare the performance of alternative investment portfolios.
  simInv tracks & displays the gross and net (after-tax and after inflation ) value of a portfolio -- a mix of assets --
  over time.

 Several kinds of assets can be specified: bonds, stocks, properties, and income and expense Streams, annuities,
 and oneOffs.

  An investment portfolio contains a set (a mix) of assets.  Different investment portfolios can contain 
  different mixes of assets.
  Each portfolio can be modified -- changing which assets it contains (or changing quantities of existing assets).
  You can modify a portfolio as often as your want. You specify the date of a modification, and its new asset mix.

  For each asset a "history" is specified -- that describes the trend (over time) of the price, interest, or
  dividend rate of the asset.

       *  On any given date: linear interpolation is used to calculate an asset's price, interest, or dividend --
          using the nearest (in time) "history" entries.
          Thus: for stable assets, an asset history does not need many entries.

   An asset's history is the same regardless of what portfolio(s) the asset may be part of.

   In short:
        *  Portfolios can grow over time -- bonds growing at an interest rate, and dividends used to purchase more of 
           a stock, and income accumulating.
           Or it could shrink, if expenses are greater than earnings!

        *  Portfolios are dynamic -- the mix of assets they contain can be modified over time.

        *  The value of each asset can change over time -- such  as the price of a stock or a property, or the interest 
           earnings of a bond.
           These changes have nothing to do with your portfolios -- they reflect what's happening in the "real world".

        *  Thus: on a given date, the value of a portfolio depends both on its asset mix; and the price, etc. of its 
           assets on that date.

  And the point is ...

     *  Portfolios are independent --  you are NOT dividing a set quantity of money across portfolios.

	Instead: you are comparing what happens to a starting investment.

        Thus: when comparing portfolios, it is useful to create them with the same starting investment (the same amount 
         invested in their asset mix).

      * When modfications are specified: simInv checks for feasibility -- are the funds available (in a portfolio on a 
        given date) able to  acquire the desired asset mix?  And that includes accounting for tax payments if assets are 
        sold.

        If you allocate too much (or too little) a special `Cash` asset is modified -- which can grow with user set 
        interest rate(s).

      *  simInv encourages honest comparisons across portfolios!
         That means that the asset histories should reflect reality; with accurate updates as time goes by.

The following briefly describes simInv.  simInv has extensive on line help -- read it for the details!

2. Details on the types of assets:

    * "bonds" : an asset that grows at an interest rate.   For example: a savings account, a CD, or bond fund.  
      Interest earnings are taxable.
      A tax-free fraction of interest earnings can be specified. For example, 1.0 for a municipal bond fund that is not 
      subject to taxes.
      Or, a Roth IRA (with 1.0 tax free fraction).

      Unless you specifically "sell" bonds (in a portfolio modification):
          The interest earnings of a bond asset are always retained (they are reinvested) -- 
          so the bond's value grows over time at the rate of after-tax-interest.

      You can also specify "yearly" additions to a bond fund -- which come out of `Cash`. Or, bonds can
      be sold and added toe `Cash`

    * "tax deferred bond" :  a bond whose earnings are tax deferred. Taxes are paid only when the "bond" is sold -- 
      and the taxes are on revenue earned when the when bonds are sold  -- not just on its interest earnings.
      For example: an IRA or a 401k

      The interest earnings of a tax deferred bond are always retained  (they are reinvested) --
      so the bond's value grows over time at the rate of interest.
 
      You can also specify "yearly" additions to a tax-deferred bond fund -- which come out of `Cash`.
      Or -- you can withdraw funds (on a yearly basis using) a required minimum distribution.

      In addition to assets whose history you explicitly specify, simInv comes with a number of "public assets" --
      stocks and funds available  on the market.

      You can add these assets to the list of "available assets" (assets that can be added to a portfolio) as needed.

   *  "stocks" : an asset that yields a dividend and whose price can change.  Dividends are taxable, as are capital 
      gains when a stock is sold.
      For example: a publically traded stock.

      The divdend earnings of a stock are always reinveseted (used to purchase more of the same stock)  - so the # of 
      shares increases over time.
      The rate of increase is a function of dividend/price -- since both can fluctuate, so can this rate of increase!

   * properties: an asset that has a price, and  Rent, that can change.

     Rent is yearly income from a property -- such as rental income minus property taxes.  If income is low and expenses
     are high, the Rent can be negative!
     Properties can be purchased with loans -- you specify the terms of the loan when you add a property asset.
         Rents, and sales of properties, are saved to `Cash` .
         Loan payments are withdrawn from `Cash`.
         You can refinance loans.

     In contrast to stocks and bonds:
       *  Rents (positive or negative) due to a property are  NOT reinvested in the property.
       *  The "value" is  obtained when the property is sold in its entirety -- after paying off remaining loan balance 
          and capital gains taxes.
       *  Fractional pieces of a property can NOT be sold.

     When sold, properties are subject to capital gains tax -- whose rate can be specified.
        For example: a vacation home  may be treated as a personal property when sold
        (hence not subject to full capital gains tax).

   * incomeStreams:  a yearly income  

      The income is taxed and the resulting revenue is added to the `Cash` asset.
      incomeStreams have no "sale" value -- when they end, the income they yields stops (with no other impact).

      Income streams can vary over time -- as specified in their asset history. 

      Examples:
        *  a part time job can be varying -- the income recieved can go up or down.

   * expenseStreams:  a yearly expense 

      expenseStreams:  are withdrawn from `Cash`.
      For tax purposes the expense can offset other incomes -- reducing your tax payments.
      expenseStreams have no "sale" value -- when they end, the expense they impose stops (with no other impact).

      expenseStreams can vary over time -- as specified in their asset history. 

      Examples:
        *  a yearly vacation
        *  yearly charitable donations -- that offset taxxable income

   * annuity: yearly income determined by a starting date
         Annuity income is taxed and the resulting revenue is added to the `Cash` asset.
         Annuities have no "sale" value -- when they end, the income they yields stops (with no other impact).

       In contrast to incomeStreams: the income flow of an annuity depends on when it is added to a portfolio.
       The asset history is used to determine the starting value of an annuity (based on the date it is added),
       and its rate of growth (as a fraction of the CPI).

       For example: social security. The amount you earn depends on when you start receiving it (with growth
       based on inflation).

	Thus: if the assetHistory has a large increase (or drop) in the "starting value" of an annuity -- and
        this change occurs AFTER the annuity is added to a portfolio ... then the yearly income from the annuity will
        NOT change.

   * oneOffs:  one off windfalls or expenses
	Unlike other simInv assets, oneOffs are single day events.

	oneOffs are added (or removed) from `Cash`. This occurs the day AFTER a oneOff is added to a portfolio.
	And, the oneOff is removed from the asset mix once it occurs. Hence they have no sale value.  

	oneOffs are not taxed. If you are adding a taxable windfall, include the tax in the oneOff's value!

	Examples: An inheritance would be positive oneOff. 
	          An unexpected home repair would be negative oneOff.


 * `Cash` : this is where non-allocated portion of your budget, and revenues (income, expenses, annuities,
     oneOffs, loan payments, ane Rents) are placed.
     These revenues can be positive (i.e.; incomes), or negative (i.e.; expenses).

      You can NOT directly modify `Cash`-- it is auto-calculated based on the performance of your asset-mix.

     `Cash` is  subject to two interest rates : one when `Cash` is greater than 0, and another when it is less than 0.
      For example:
            a very low rate for positive `Cash` balances (for example, 0.1% in a savings account),
            a high rate for negative `Cash` balances (for example, 11.5% for a credit card).

     Assuming the above:
        it is best  to have enough `Cash` to cover expenses (such as loan payments), but not much more (or less).
        That means it is useful to modify your portfolio regularly -- selling or purchasing assets as your 
        `Cash` balance changes

 	Hint: you can use additions (of regular or tax-deferred bonds) to move funds into Cash on a yearly basis.

3. Installation:

  simInv can be run in two modes:

    * online mode --  requires a server that supports php 7.0 or above.
    * in standalone mode -- can be run directly from a browser accessing a file on your computer

   Advantages and disadvantages

      onLine mode
       * Accessible from anywhere via the web
       * Users do not have to install the simInv package on their own computer.
       * Requires installation on a http: (or https:) server that
            i) supports php 7.0 or above
           ii) allows php to write files to a directory
       * Users do not have to worry about data file maintenance (though archiving is recommended).
       * Security is not great -- though encryption can help.
       * Public assets can be modified (by the server admin).

     standAlone mode
       * Accessible from a user's computer -- a file:// url is used
       * Users must install the simInv package on their own computer.
       * Does NOT require a server -- and does not require php
       * Uses local data storage using indexDB. Some browser installations may not enable local data storage
       * Data storage is browser-on-a-computer specific.
       * Users are responsible for maintaining data files. Archiving data to local files requires a few steps.
       * Fairly secure, so long as users control access to their computer
       * Anyone with access to this computer can view all of the simInv users (who are using the same computer)
       * Public assets can not be easily modified.

     A hybrid mode is also available: onLine access with local storage.
       * Accessible from anywhere via the web
       * Users do not have to install the simInv package on their own computer.
       * Requires installation on a http: (or https:) server that
            i) supports php 7.0 or above
           ii) but does not use php to write files to a directory
       * Uses local data storage. Some browser installations may not enable local data storage
       * Users are responsible for maintaining data files. Archiving data to local files requires a few steps.
       * Fairly secure, so long as users control access to their computer
       * Anyone with access to this computer can view all of the simInv users (who are using the same computer)
       * Public assets can  be modified (by the server admin).


3a.  Installing in onLine mode.

    The simInv administrator should

      a) Create a simInv directory in a web accessible directory
      b) Unzip simInv_vxxx.zip to this directory.

      Several subdirectories are created.
      Of particular interest are: 
         data/ : where user data is stored.
         publicAssets/  : where specifications for "public" assets are stored 
  	 archive/  : not directly used by simInv.  It's a convenient place to place archive files  

     c)     The data/ directory will contain subdirectories for each user.

        ***   It is the administrators job to create directories for each recognized user.  ***

       For example: for user "joeb" the admin should create data/joeb

       Note: simInv comes with a "test" user specified. You can use it for testing and demo purposes!

    d)  Load index.html with your favorite javascript capable browser.
        For example: http://mysite.org/simInv/index.html
  Users should logon with one of the usernames created in step (c). On their first logon, simInv will initialize
  their account -- and ask if they want to use encryption.


3b. Installing in standAlone mode

    a) The user should unzip simInv_vxxx.zip to an empty directory.
       For example: d:/myStuff/simInv
       Note that several directories (such as  data/ and publicAssets) are created, but data/ is not
       used in standAlone mode.

    b) In your browser, enter a file:/// url to index.html.
         For example: file:///d:/myStuff/simInv/index.html

    c) Enter a username. The first time, simInv will initialize simInv data for this data -- using local storage.
       An individual (or several individual) using a given computer can use as many usernames as desired --
       each username data is stored seperately

3c. Installing in onLine mode with local storage.
    Users do NOT have to download the simInv package, but need accesss to the web to load it 
    (using a http://.../simInv/simInv.html url).

    As with onLine mode installation...
      a) Create a simInv directory in a web accessible directory
      b) Unzip simInv_vxxx.zip to this directory.

      c) Using a text editor, edit index.html  (in the directory where simInv was installed), and set the
        "global variable":
           onLineLocalStorage=1 ;
        This should be around line 20.

  As with onLine mode, users will load index.html from the web (using something like  http://.../simInv.html)
  However: as with standAlone mode -- all data for a user will be stored on their computer.

  Notes:

    * in 'onLine with local storage' mode -- the admin does NOT need to create directories under
       data/ for allowed users.

    * local data storage depends on how you access simInv.

      In particular: accessing simInv using a file:/// url or via the web (with onLineLocalStorage=1) uses seperate
      data files.
      For example: user data when accessing index.html via  file:///pathToSimInv/index.html will NOT be available when
      accessing index.html via the web -- even though both methods store the data on the same computer!

     It also depends on which browser you are running on a given computer!
     For example: simInv local data stored when using FireFox will NOT be available when you use Chrome.
.
    * you can use export and import to move a user`s simInv data across modes.

    * some browsers do not support indexDB local storage.

    Advanced users hint:
       You can allow users to choose which onLine storage mode (onLine or local) when they first logon.
       See below for the details.

3c.  Removing users, and clearing data

To remove a user ..

 *  onLine storage -- requires access to simInv directory on the server

       i) In simInv/data : find the subdirectory for the use
     ii) Erase all its files!
        The next time the user logs in, she will be asked to initialize.
    iii) Or, remove the directory -- the user will not be allowed to login

 *  local storage mode -- anyone with access to the computer (that simInv is using for local storage)
       i ) logon as the desired user
      ii) Click status icon (in the upper right corner) for a menu
     iii) Click the 'remove this user' button on the page that appears

    Hint: you can switch to another user (on this computer) using the list of users (at the bottom of
         this menu).  
         In onLine mode with user chosen storage: you can remove a user who chose onLine storage.
         Removing this kind of user does NOT delete their "server stored" simInv data -- but they
         will have to relogon to simInv (and choose onLine storage) to regain access.

    That means: anyone with access to this computer can see data for all users. And they can delete


3d. Selecting storage modes         

   simInv can give users the choice between storge methods in onLine mode.
   The user chooses which mode when she first logons -- and this mode is used for all future logons. 

  To enable this, in simInv/index.html set the following variables (around line 10)

      var onLineLocalStorage=2  ;

  Note that in standAlone mode -- the user does NOT have a choice of storage modes  (local storage must be used).

  On the first logon to simInv, a menu will be shown asking what storage method to use.
   And this method will be used for all future logons by this user.

3e. Clearing local storage

   If local storage needs to be cleared, you can use browser tools.
    Example: for Firefox
	    i) Logon to simInv in your normal fashion
           ii) Hit the F12 key (or RMB on the page and select `Inspect (Q)`)
          iii) Click the `storage` choice on the button bar
           iv) Click on `Local Storage`
           v) RMB on your site
          vi) Select "Delete all"

   Hints:
     *  archive user data beforehand, so you can restore them (after changing the storage mode).

3f. Updating schedules

  simInv comes with some "schedules" -- such as CPIU and RMDs -- that can be changed by the administrator.
  For example, if a new year of CPIU is released.
  See simInv_schedules.js!

3g. Updating public assets
 
    In online mode, it is not difficult for the server admin to add (or modify existing) public assets.
    See publicAssets/readme.txt for the details.


4.  Using simInv  .....

   While not required, each user may want to change the personal settings when they logon after initialization 
   is completed.
         The first time a user logons on, a few initialization steps are taken. 
         The steps depend on whether onLine or standAlone mode is used.

   In either case: after succesfully logging on  and initializing, a user may want to change his personal settings.

   User should then create their own assets and portfolios.
   This can be done at any time -- with new assets and new portfolio mixes added as convenient.
   But use some caution: specifying a modification with a date that is in between existing modifications can have odd
   effects on porfolio specification.
   Similarly, revising  an asset history  -- adding entries that occur before the specified date of an existing
   modification -- can have odd effects.

   The online help outlines how to work with asset and portfolios.

  Notes:
    * admins can add "publicAssets" -- assets whose attribute and history come with simInv's distribution.
      See publicAssets/readme.txt for instructions on how to add publicAssets  
    * simInv_params.js specifies the default personal settings. It also specified some generic settings (that 
      can not be personallized).
    * The admin (or user, in standAlone mode) can modify these several .js files, andn index.html.
      If an error occurs, backups of these files are in the other/ subdirectory (look for fileName.original)


Limitations:

   simInv has a relatively simple inflation model -- using a yearly CPI series for all values (that is specified in
   simInv_schedules.js).

   It is recommended that all values (such as prices, etc in the asset historys) be entered as actual values
   (not inflation adjusted).

   simInv has a fairly simple algorithim for accounting for taxes.
        Taxes on earnings (interest from bonds, dividends from stocks) are collected on a "daily" basis.
        Capital gains taxes on sales of properties and stocks are collected when they occur (on the modification date).
        date). And taxes on sale of tax-deferred bonds are collected when they occur (on the modification date).

        Negative capital gains can offset positive capital gains (to reduce capital gains tax), but can not be
        transferred to other sources of income.
        Capital gains occur when properties and stocks are sold -- the sum of all these sales (minus their basis) is
        used to compute a capital gains tax.
 

        The total revenue (across all incomeStreams, annuities, and netRents) is used to calculate taxes.

       expenseStream tax offsets are directly applied to the expense. For example, if the tax rate is 20%, and an
        expense has a 80% tax-offset ...  then 84% of the expense is "charged" to `Cash`.

       Changes in tax-deferred bonds can offset (so moving from one tax-deferred bond to another will not require
       paying  a tax).
       But a modification that leads to a net decrease in the aggregate value of a portfolio's tax-deferred bonds will
       be taxed (even if the next day this decrease is reallocated to a tax-deferred bond).

   simInv, when run in onLine mode, is not very secure

       However, simInv can encrypt all data saved on the server -- which requires that the user specify, and remember,
       an encryption key.

       This will improve security -- someone with access to the server's files will not be able to easily read your
       data.  Note that simInv encryption is not guaranteed to be safe against all attacks (such as man in the
       middle attacks).

       In standAlone mode simInv should be fairly secure -- assuming you control access to your computer.
       simInv ver 1.8 does not support encryption of locally stored data.

   simInv uses some approximations to calculate revenues, taxes, and growth.
     These can be less accurate if time spans between modifications are large (say, several years long).

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

    Note: although encryption can help, in general simInv uses security measures that are not strong.
          In particular: if you do not control access to the directory that simInv
                         (index.html, simInv2.php, and other files) is installed on  ...
                     --  you should NOT install simInv on your web server, or on your personal computer!

