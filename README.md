# issapitestrunner

# Running the Test Suite for ISS Satellite APIs

# Steps:
1. Install git and setup in local using link -> https://github.com/git-guides/install-git
2. Install node and npm and setup in local using link -> https://docs.npmjs.com/downloading-and-installing-node-js-and-npm
3. Create a folder gitrepo and clone the repo https://github.com/rohitsingh3688/issapitestrunner.git using below command:
    git clone https://github.com/rohitsingh3688/issapitestrunner.git
4. Open windows command prompt, go to the above folder location gitrepo/issapitestrunner and run below command
    npm install
5. To run the postman test and generate report locally, run below command
    npm run report1 && npm run report2
6. To access the report, please go to gitrepo/issapitestrunner/newman folder and check the 2 html reports created for both the APIs below
   https://api.wheretheiss.at/v1/satellites/25544/tles
   https://api.wheretheiss.at/v1/satellites/25544/positions?timestamps=1436029892,1436029902&units=miles
7. To check the report from clound cli, please login to below url and click on build link below the first pipeline row, then click on Artifacts tab and click on the html          reports
   https://app.circleci.com/pipelines/github/rohitsingh3688/issapitestrunner
   
# Issues with API observed so far

1. API -> https://api.wheretheiss.at/v1/satellites/25544/tles
    a. Doesn't validate the format values for invalid data or blank values or invalid format passed in the query parameter and always returns 200 irrespective instead of 400
    b. Doesn't validate the format of the satellite id and always returns 404 instead of 400
    c. Accepts any query parameters in the url apart from the format query parameter instead of throwing 400
    d. Accepts any random separator for query values like # instead of , and doesnt return 400 instead of 200
    
2. API -> https://api.wheretheiss.at/v1/satellites/25544/positions?timestamps=1436029892,1436029902&units=miles
    a. Doesn't return any error message for Invalid Unit format, values or multiple units passed nor returns 400
    b. Doesn't return all the invalid timestamps in the error message when one or more invalid timestamps are returned
    c. Doesn't validate the format of the satellite id and always returns 404 instead of 400
    d. Accepts any query parameters in the url apart from the timestamps and units query parameter instead of throwing 400
    e. Doesn't validate the range of timestamps values and hence returns 500 for very big timestamp value instead of 400
    f. Accepts more than 10 timestamps even though it is supposed to accept only 10 timestamps in one call
    g. Accepts any random separator for query values like # instead of , and doesnt return 400 instead of 200
    h. Accepts more than one units in the units query parameter instead of 1 and only returns kilometers in those cases
    i. Accepts duplicates in timestamps query parameter and returns duplicate records instead of 1 unique record
    j. Returns incorrect error message when timestamps is sent as arrays [1234,4567]
   


