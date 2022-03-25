# Rossmann Sales Prediction

<img src=Images/rossmann.jpg width="650" height="200"/>

<p><strong>Disclaimer</strong>: this project was based on the &quot;Rossmann Store Sales&quot; challenge published on <a href="https://www.kaggle.com/c/rossmann-store-sales">Kaggle</a>. It is a fictitious project. However; the steps followed to solve the business problem are the same applied to real projects.</p>

<h1 dir="auto">Business problem</h1>

<p dir="auto">The CFO of Rossmann Drug Stores requested a sales prediction for each store for the next six weeks in order to define a budget for stores refurbishment. The resources would be allocated according to each store's sales prediction. The current prediction is not satisfactory as there are several inconsistencies. </p>

<h3 dir="auto">Solution Proposal</h3>
<p>In this context, I developed a machine learning model in order to provide a more accurate store sale forecast.</p>

<h1 dir="auto">Dataset Summary</h1>
<p>The dataset provides historical sales data for 1,115 Rossmann stores. The dataset is available on <a href="https://www.kaggle.com/c/rossmann-store-sales">Kaggle</a>.</p>


<table style="width: 100%;">
    <tbody>
        <tr>
            <td style="width: 39.0229%;">
                <div style="text-align: left;"><strong>Attribute</strong></div>
            </td>
            <td style="width: 60.9771%;">
                <div style="text-align: left;"><strong>Description</strong></div>
            </td>
        </tr>
        <tr>
            <td style="width: 39.0229%; vertical-align: bottom;">Id</td>
            <td style="width: 60.9771%;">An Id that represents a (Store, Date) duple within the test set</td>
        </tr>
        <tr>
            <td style="width: 39.0229%; text-align: left; vertical-align: bottom;">Store</td>
            <td style="width: 60.9771%;">A unique Id for each store</td>
        </tr>
        <tr>
            <td style="width: 39.0229%; vertical-align: bottom;">Sales<br></td>
            <td style="width: 60.9771%;">The turnover for any given day (this is what you are predicting)<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%; vertical-align: bottom;">Customers<br></td>
            <td style="width: 60.9771%;">The number of customers on a given day<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%; vertical-align: bottom;">Open<br></td>
            <td style="width: 60.9771%;">An indicator for whether the store was open: 0 = closed, 1 = open<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%; vertical-align: bottom;">StateHoliday<br></td>
            <td style="width: 60.9771%;">Indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%; vertical-align: bottom;">SchoolHoliday<br></td>
            <td style="width: 60.9771%;">Indicates if the (Store, Date) was affected by the closure of public schools<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%;vertical-align: bottom;">StoreType<br></td>
            <td style="width: 60.9771%;">Differentiates between 4 different store models: a, b, c, d<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%;vertical-align: bottom;">Assortment<br></td>
            <td style="width: 60.9771%;">Describes an assortment level: a = basic, b = extra, c = extended<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%;vertical-align: bottom;">CompetitionDistance<br></td>
            <td style="width: 60.9771%;">Distance in meters to the nearest competitor store<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%;vertical-align: bottom;">CompetitionOpenSince[Month/Year]<br></td>
            <td style="width: 60.9771%;">Gives the approximate year and month of the time the nearest competitor was opened<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%;vertical-align: bottom;">Promo<br></td>
            <td style="width: 60.9771%;">Indicates whether a store is running a promo on that day<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%;vertical-align: bottom;">Promo2<br></td>
            <td style="width: 60.9771%;">Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%;vertical-align: bottom;">Promo2Since[Year/Week]<br></td>
            <td style="width: 60.9771%;">Describes the year and calendar week when the store started participating in Promo2<br></td>
        </tr>
        <tr>
            <td style="width: 39.0229%;vertical-align: bottom;">PromoInterval<br></td>
            <td style="width: 60.9771%;">Describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. &quot;Feb,May,Aug,Nov&quot; means each round starts in February, May, August, November of any given year for that store<br></td>
        </tr>
    </tbody>
</table>


<h1 dir="auto">Business Assumptions</h1>
<ul dir="auto">
    <li>The days the stores were closed were removed from the analysis.</li>
    <li>Only stores with sales values bigger than 0 were considered.</li>
    <li>For stores that did not have Competition Distance information, it was considered that the distance should be 200,000 - higher than the longest distance observed in the data set. This assumption represents that the closest competitor might be too far to computethere, or there is no competition at all. </li>
</ul>

<h1 dir="auto">Solution methodology</h1>
<p dir="auto">The solution was developed based on the CRISP (CRoss-Industry Standard Process for data mining) methodology, which is a cyclical approach that streamlines the delivery of value.</p>
<img src=Images/CRISP.png/>
<p>Source: <a href="https://commons.wikimedia.org/wiki/File:CRISP-DM_Process_Diagram.png">Wikimedia</a>&nbsp;</p>

<p dir="auto"><strong>Step 01</strong>. <strong>Data Description:</strong> Using statistical metrics to identify outliers in the business scope and also analyze basic statistical metrics such as: mean, median, maximum, minimum, range, skew, curtosis and standard deviation.</p>
<p dir="auto"><strong>Step 02</strong>. <strong>Feature Engineering</strong>: Obtaining new attributes based on the original variables, in order to better describe the phenomenon to be modeled.</p>
<p dir="auto"><strong>Step 03</strong>. <strong>Data Filtering</strong>: Filtering rows and delete columns that are not relevant for the model or are not part of the business scope.</p>
<p dir="auto"><strong>Step 04</strong>. <strong>Exploratory Data Analysis</strong>: Exploring the data to find insights and better understand the impact of variables on model learning.</p>
<p dir="auto"><strong>Step 05</strong>. <strong>Data Preparation</strong>: Preparing the data for the machine learning application.</p>
<p dir="auto"><strong>Step 06</strong>. <strong>Feature Selection</strong>: Selecting the best attributes to train the model. It was used Boruta Algorithm to make the selection.</p>
<p dir="auto"><strong>Step 07</strong>. <strong>Machine Learning Modeling</strong>: Training the Machine learning model.</p>
<p dir="auto"><strong>Step 08</strong>. <strong>Hyperparameter Fine Tunning</strong>: Choosing the best values for each of the parameters of the model selected in the previous step.</p>
<p dir="auto"><strong>Step 09</strong>. <strong>Convert model performance to business values</strong>: Converting model performance to a business result.</p>
<p dir="auto"><strong>Step 10</strong>. <strong>Deploy Model to Production</strong>: Publishing the model in a cloud environment so that other people or services can use the results to improve the business decision. The cloud application platform choosed was Heroku.</p>
<p dir="auto"><strong>Step 11</strong>. <strong>Telegram Bot</strong>: Creating a bot on the telegram app, that make possible to consult the forecast at any time.</p>

<h1 dir="auto">Hypotheses Mind Map </h1>
<p>A Mind Map was created to generate hypothesis that would turn into insights during the Exploratory Data Analysis.</p>
<img src=Images/MindMap_Hypothesis.png/>
<p dir="auto"><br></p>

<ol dir="auto">
<p><strong>H1.</strong> Stores with a bigger product assortment are more likely to sell more daily</p>
<p><strong>H2.</strong> Stores with closer competitors are more likely to sell less</p>
<p><strong>H3.</strong> Stores with longer-standing competitors are more likely sell more</p>
<p><strong>H4.</strong> Products on sales during a long period of time are more likely to sell more daily</p>
<p><strong>H5.</strong> Stores with more extended promotions are more likely to sell more</p>
<p><strong>H6.</strong> Sales are more likely to increase during holiday season (Christmas)</p>
<p><strong>H7.</strong> Stores are more likely to sell more over the years</p>
<p><strong>H8.</strong> Stores are more likely to sell more in the second half of the year</p>
<p><strong>H9.</strong> Stores are more likely to sell more after the 10th day of each month</p>
<p><strong>H10.</strong> Stores are more likely to sell less on weekends</p>
<p><strong>H11.</strong> Stores are more likely to sell less during school holidays</p>

</ol>
<p dir="auto">Please find the summary of the analysis of hypotheses 1, 2, 5. Refer to the notebook file for the complete Exploratory Data Analysis.<br></p>

<h1 dir="auto">Top Three Data Insights </h1>
<p><strong>H1.</strong> **Stores with a bigger product assortment are more likely to sell more daily**</p>
<p>**True**: Stores with a bigger product assortment are more likely to sell more</p>
<img src='Images/H1.png'.png/>
<p><br></p>
<p>Stores with extra assortment have a better performance when comparing the average sales over time between all story types.</p>
<img src='Images/H1_1.png'.png/>

<p><br></p>

<p><strong>H2.</strong> **Stores with closer competitors are more likely to sell less**</p>
<p>**False**: The distance from competitors does not influence store sales.</p>
<p>Notice that sales do not increase as the nearest competitor distance grow. Sales seem to be independent of competition distance, which can be considered an insight. Competitor does not impact the business negatively, contradicting the common belief.</p>
<img src='Images/H2_2.png'.png/>


<p><br></p>

<p><strong>H5.</strong> **Stores with more extended promotions are more likely to sell more**</p>
<p>**False**: Stores that applied promo2 followed by promo1 performed worse on average when compared to stores that applied only the promo1.</p>

<p>Historically, following this approach do not work in terms of generating more sales.</p>
<img src='Images/H3.png'.png/>


<h1 dir="auto">Tested Machine Learning Models</h1>
<ul dir="auto">
    <li>Average Model (Baseline)</li>
    <li>Linear Regression Model</li>
    <li>Linear Regression Regularized Model (Lasso)</li>
    <li>Random Forest Regressor</li>
    <li>XGBoost Regressor</li>
</ul>

<h1 dir="auto">Machine Learning Models Performance</h1>

<p>The metrics applied to measure the performance of the algorithms were MAE, MAPE and RMSE.</p>

<h1 dir="auto">Hyperparemeter Fine Tuning</h1>

<h1 dir="auto">Business Performance</h1>
