# Rossmann Sales Prediction

<img src=Images/rossmann.jpg width="650" height="200"/>

<p><strong>Disclaimer</strong>: this project was based on the &quot;Rossmann Store Sales&quot; challenge published on <a href="https://www.kaggle.com/c/rossmann-store-sales">Kaggle</a>. It is a fictitious project. However; the steps followed to solve the business problem are the same applied to real projects.</p>

<h1 dir="auto">Business problem</h1>

<p dir="auto">The CFO of Rossmann Drug Stores requested a sales prediction for each store for the next six weeks in order to define a budget for stores refurbishment. The resources would be allocated according to each store's sales prediction. The current prediction is not satisfactory as there are several inconsistencies. </p>

<h3 dir="auto">Solution Proposal</h3>
<p>A machine learning model was developed to provide a more precise store sale forecast.</p>

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
<p><strong>H1. Stores with a bigger product assortment are more likely to sell more daily</strong></p>
<p><strong>True:</strong> Stores with a bigger product assortment are more likely to sell more</p>
<p>Stores with extra assortment have a better performance when comparing the average sales over time between all story types.</p>
<img src='Images/H1_1.png'/>
<p><br></p>

<p><strong>H2.Stores with closer competitors are more likely to sell less</strong></p>
<p><strong>False</strong>: The distance from competitors does not influence store sales.</p>
<p>Notice that sales do not increase as the nearest competitor distance grow. Sales seem to be independent of competition distance, which can be considered an insight. Competitor does not impact the business negatively, contradicting the common belief.</p>
<img src='Images/H2_2.png'.png/>
<p><br></p>

<p><strong>H5. Stores with more extended promotions are more likely to sell more</strong></p>
<p><strong>False:</strong> Stores that applied promo2 followed by promo1 performed worse on average when compared to stores that applied only the promo1.</p>

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

<p>The metrics applied to measure the performance of the algorithms were MAE, MAPE and RMSE. </p>
<ol>
    <li>MAE<em>&nbsp;(Mean Absolute Error)&nbsp;</em></li>
    <li><em>MAPE</em> (Mean Absolute Percentage Error)</li>
    <li>RMSE<em>&nbsp;(Root Mean Squared Error) </em></li>
</ol>
<p>The Cross-Validation resampling procedure was applied to each ML model to provide a more reliable performance overview. Please find the results in the table below:</p>
<div align="left">
    <table style="margin-right: calc(11%); width: 89%;">
        <tbody>
            <tr>
                <td style="width: 36.4386%;">
                    <p><strong>Model Name</strong></p>
                </td>
                <td style="width: 23.645%;">
                    <p><strong>MAE</strong></p>
                </td>
                <td style="width: 17.9539%;">
                    <p><strong>MAPE</strong></p>
                </td>
                <td style="width: 21.8401%;">
                    <p><strong>RMSE</strong></p>
                </td>
            </tr>
            <tr>
                <td style="width: 36.4386%;">
                    <p>XGBoost Regressor</p>
                </td>
                <td style="width: 23.645%;">
                    <p>1056.17 +/- 179.13</p>
                </td>
                <td style="width: 17.9539%;">
                    <p>0.14 +/- 0.02</p>
                </td>
                <td style="width: 21.8401%;">
                    <p>1528.68 +/- 247.36</p>
                </td>
            </tr>
            <tr>
                <td style="width: 36.4386%;">
                    <p>Random Forest Regressor</p>
                </td>
                <td style="width: 23.645%;">
                    <p>1752.72 +/- 247.1</p>
                </td>
                <td style="width: 17.9539%;">
                    <p>0.24 +/- 0.01</p>
                </td>
                <td style="width: 21.8401%;">
                    <p>2477.31 +/- 347.8</p>
                </td>
            </tr>
            <tr>
                <td style="width: 36.4386%;">
                    <p>Linear Regression</p>
                </td>
                <td style="width: 23.645%;">
                    <p>2082.69 +/- 294.85</p>
                </td>
                <td style="width: 17.9539%;">
                    <p>0.3 +/- 0.02</p>
                </td>
                <td style="width: 21.8401%;">
                    <p>2953.48 +/- 467.23</p>
                </td>
            </tr>
            <tr>
                <td style="width: 36.4386%;">
                    <p>Linear Regression - Lasso</p>
                </td>
                <td style="width: 23.645%;">
                    <p>2116.16 +/- 340.55</p>
                </td>
                <td style="width: 17.9539%;">
                    <p>0.29 +/- 0.01</p>
                </td>
                <td style="width: 21.8401%;">
                    <p>3057.36 +/- 503.47</p>
                </td>
            </tr>
        </tbody>
    </table>
</div>

<p>The ML model chosen to continue the analysis and calculate the predictions is the XGBoost Regressor, as this model had the best performance. Another advantage of using XGBoost Regressor is that XGBoost Regressor requires less memory than RandomForest when deployed to production.</p>

<h1 dir="auto">Hyperparemeter Fine Tuning</h1>
<p>The Random Search procedure was used to optimize the Hyperparemeters of XGBoost Regressor. When applying the optimized parameters found out by Random Search to XGBoost Regressor, the performance on the test dataset was:</p>

<div align="left"><br></div>
<div align="left">
    <table>
        <tbody>
            <tr>
                <td>
                    <p><strong>Model Name</strong></p>
                </td>
                <td style="width: 26.9886%;">
                    <p><strong>MAE</strong></p>
                </td>
                <td style="width: 22.0729%;">
                    <p><strong>MAPE</strong></p>
                </td>
                <td style="width: 14.2035%;">
                    <p><strong>RMSE</strong></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>XGBoost Regressor</p>
                </td>
                <td style="width: 26.9886%;">
                    <p>635.79</p>
                </td>
                <td style="width: 22.0729%;">
                    <p>0.092</p>
                </td>
                <td style="width: 14.2035%;">
                    <p>930.88</p>
                </td>
            </tr>
        </tbody>
    </table>
</div>

<h1 dir="auto">Business Performance</h1>
<p>These are the methods used to evaluate the Machine Learning prediction model in terms of business results:</p>

<p><strong>Analysis of divergence between the sales predicted and real sales.</strong></p>
<p>The graph bellow presents the stores&apos; MAPE:</p>
<p><img src="Images/MAPE.png"><br></p>
<p>Notice that most predictions are centered around a line parallel to the X axis (MAPE 9% in Y axis). However, there are points quite far apart. Some stores&apos; forecasts are not accurate. Stores where the value prediction diverge significantly from the real sales are not recommended to make business decisions based on the current model.</p>
<p><strong>How much the model predicted each store to sell in the expected scenario, worst scenario and best scenario.</strong></p>
<table>
    <tbody>
        <tr>
            <td>
                <p><strong>store</strong></p>
            </td>
            <td>
                <p><strong>predictions</strong></p>
            </td>
            <td>
                <p><strong>worst_scenario</strong></p>
            </td>
            <td>
                <p><strong>best_scenario</strong></p>
            </td>
            <td>
                <p><strong>MAE</strong></p>
            </td>
            <td>
                <p><strong>MAPE</strong></p>
            </td>
        </tr>
        <tr>
            <td>
                <p>1</p>
            </td>
            <td>
                <p>163903.87</p>
            </td>
            <td>
                <p>163623.30</p>
            </td>
            <td>
                <p>164184.44</p>
            </td>
            <td>
                <p>280.57</p>
            </td>
            <td>
                <p>0.063</p>
            </td>
        </tr>
        <tr>
            <td>
                <p>2</p>
            </td>
            <td>
                <p>179493.82</p>
            </td>
            <td>
                <p>179113.18</p>
            </td>
            <td>
                <p>179874.47</p>
            </td>
            <td>
                <p>380.64</p>
            </td>
            <td>
                <p>0.076</p>
            </td>
        </tr>
        <tr>
            <td>
                <p>3</p>
            </td>
            <td>
                <p>261257.82</p>
            </td>
            <td>
                <p>260702.46</p>
            </td>
            <td>
                <p>261813.19</p>
            </td>
            <td>
                <p>555.36</p>
            </td>
            <td>
                <p>0.077</p>
            </td>
        </tr>
        <tr>
            <td>
                <p>4</p>
            </td>
            <td>
                <p>343334.03</p>
            </td>
            <td>
                <p>342475.49</p>
            </td>
            <td>
                <p>344192.56</p>
            </td>
            <td>
                <p>858.53</p>
            </td>
            <td>
                <p>0.081</p>
            </td>
        </tr>
    </tbody>
</table>

<p><strong>Analysis of predicted daily sales behavior in the analyzed period, for all stores sales.</strong></p>
<img src='Images/Predict_Over_Time.png'/>
<p>The shadow indicates that multiple stores were ploted over time.</p>

<h1 dir="auto">Deployment</h1>
<div align="left">At this stage, the model will be put into production to make the predictions accessible to the end user. A telegram bot will be designed so anyone access the sales prediction of any store.</div>
<img src='Images/API_scheme.png'/>
<p>The user will send a request to Rossmann API through telegram using a code such as a store number. Rossmann receives the code, loads the Test Dataset, and filter only the features of the specified store.</p>
<p>This info is sent from Rossmann API to API Handler along with a request for sales prediction. The API Handler accesses the Data Preparation file and loads the trained model to return the result.</p>
<h2>Telegram </h2>
<p>Send the store number and get the sales prediction for the next six weeks.</p>
<img src="Images/Telegram.jpg" style="width: 280px; height: 560px;"/>
<p>chatbot id: @rossmann_modelprediction_bot</p>


<h1 dir="auto">Conclusion</h1>

<p>Overall, the model developed had a good performance and the results satisfied the company requirements. Following the CRISP methodology, the next step is to analyze the stores with bad performance to increase the accuracy of the sales forecast. New Machine Learning models could be applied. However, the time and resources allocated to a new cycle should be taken into account. </p>
