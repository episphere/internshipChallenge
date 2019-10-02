# NCI DCEG Internship Challenge

Here's a data analysis challenge for you that is similar to the stuff we do at DCEG. Like most analytical problems in data science, there is no single correct answer, and the effectiveness of your solution will largely depend on your understanding of the data. Note that there is no time limit to solve the problem, but it should not take you more than 4-5 hours to design and implement your solution. 



## Problem Statement

We need to analyze the Disease Indicators behind Cancer across multiple variables and display our analyses in the form of visualizations on a web dashboard. To do this, we shall leverage the deidentified Hospital Inpatient Discharges dataset made available by the state of New York. The dataset can be found here: 

[https://health.data.ny.gov/Health/Hospital-Inpatient-Discharges-SPARCS-De-Identified/gnzp-ekau](https://health.data.ny.gov/Health/Hospital-Inpatient-Discharges-SPARCS-De-Identified/gnzp-ekau)

and the raw data can be found at the below URLs:

JSON: [https://health.data.ny.gov/resource/gnzp-ekau.json](https://health.data.ny.gov/resource/gnzp-ekau.json)

CSV: [https://health.data.ny.gov/resource/gnzp-ekau.csv](https://health.data.ny.gov/resource/gnzp-ekau.csv)

(These URLs only return 1000 observations at a time by default)

This dataset contains over 2 million observations of patients, including their characteristics, diagnoses and treatments. It has data across medical ailments, but since we only wish to perform our analyses on cancer diagnoses, we can considerably reduce the size of the dataset by using this as our base data instead:

[https://health.data.ny.gov/resource/gnzp-ekau.json?\$where=UPPER(ccs_diagnosis_description) like '%25CANCER%25'&\$limit=10](https://health.data.ny.gov/resource/gnzp-ekau.json?\$where=UPPER(ccs_diagnosis_description)%20like%20%27%25CANCER%25%27&\$limit=10)

\(Check the [Examples](#Examples) to understand how this URL is formed.)
This is actually a REST API that allows you to efficiently query the dataset. There are several such operations that you can run on the data merely by changing the query parameters in the API. You can find documentation on how to use the API here:

[https://dev.socrata.com/foundry/health.data.ny.gov/gnzp-ekau](https://dev.socrata.com/foundry/health.data.ny.gov/gnzp-ekau)

The first thing you should do is to _**Sign up for an app token**_ on the page that opens up. This token will allow you to make calls to the API without having to worry about being restricted. The documentation contains more info about how to use the token, along with helpful information about the columns in the dataset. 

You might find that there are a few fields in even the reduced dataset that are irrelevant to your analyses (such as perhaps the _operating_certificate_number_), and you may choose to disregard those fields or remove them from the base dataset you use in your analysis.

Your task is to use this data and create meaningful visualizations from it, be it in the form of histograms, line graphs, pie charts or any other you deem suitable for the analysis. These visualizations should be placed on a webpage that can be seen in a browser.

_Note: You could of course write your own functions to perform querying on the entire data yourselves, which would be completely fine by us. However, this is meant to be a fairly low-effort challenge, so we recommend that you leverage the functionality provided by the API as much as possible, and only perform your own queries when the API cannot provide you what you need._



## Submission
Your code must be available as a GitHub repository, and you need only send us the URL to the repository with your application.
For bonus points, you can host the dashboard you create on a free hosting service (such as [GitHub Pages](https://pages.github.com/) or [Heroku](https://www.heroku.com/)) and add the URL where it is hosted to your README file on GitHub.



## Evaluation Criteria

- **Please note again that this is meant to be a short exercise**, so do not spend too much time cleaning the dataset.
- Although using Python/Pandas or other languages and frameworks is not a dealbreaker, we highly recommend using JavaScript to implement your solution. Libraries like [plotly.js](https://plot.ly/javascript/), [Chart.js](https://www.chartjs.org/) should make it easy for you to design your visualizations directly for the browser.
- Your code must include: a) interactions with the API and the queries you used, b) any filtering of the data you did yourself, and c) how you generated the visualizations from that data.
- Code quality and the analyses that you run will be what you will be primarily evaluated on. Interactive visualizations will earn big ups!
- Do not fret too much about making it pretty -- color schemes, or any CSS other than the most basic stuff will not carry any points. We will only test it on Chrome, so do not worry about cross-browser compatibility either. 
- You should not need to write any backend code for this problem, though if you feel you need a server running, you should include the code for it with your submission. Be sure to mention this in your README, along with the instructions on how to run it.



## Examples
- **Using the API**: You might have noticed that the base URL for the raw dataset and the one we used to reduce it to include only cancer patients is the same -- all that was added to the URL in the latter case were the query parameters. There are 2 query parameters that we used in this case:

`$where - defines the field(s) and the condition(s) to filter the data on`

`$limit - defines how many observations to return`

We used the **\$where** clause to check for the presence of the word "cancer" in the patient's diagnosis (the _ccs_diagnosis_description_ field in the dataset).

- **Visualizations**: Examples of some basic analyses you could run might be:

  - Mortality rates across different types of cancers
  - Prevalence of cancer diagnoses among people with various racial and/or ethnic backgrounds
  - Frequency of the different types of cancers within age groups, and correlation of specific types with specific age groups

None of these are mandatory, and you may choose to create your own. There is no limit on the number of visualizations, but anywhere between 2 and 5 should be good -- just ensure that they are not repetitive.