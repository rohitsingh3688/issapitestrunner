# issapitestrunner

# Running the Test Suite for ISS Satellite APIs

# Steps:
1. Install git and setup in local using link -> https://github.com/git-guides/install-git
2. Install node and npm and setup in local using link -> https://docs.npmjs.com/downloading-and-installing-node-js-and-npm
3. Create a folder gitrepo, navigate inside the folder and clone the repo https://github.com/rohitsingh3688/issapitestrunner.git using command :
    git clone https://github.com/rohitsingh3688/issapitestrunner.git
4. Open windows command prompt, go to the above folder location gitrepo/issapitestrunner and run command
    npm install
5. To run the postman test and generate report locally, run below command
    npm run report1 && npm run report2
6. To access the report, please go to gitrepo/issapitestrunner/newman folder and check the 2 html reports created for both the APIs below
   satellite/[id]/positions
   satellite/[id]/tles
7. To check the report from clound cli, please login to below url and click on build link below the first pipeline row, then click on Artifacts tab and click on the html          reports
   https://app.circleci.com/pipelines/github/rohitsingh3688/issapitestrunner
8. Additionaly if you have the postman locally and want to run the collection then import the collection from folder issapitestrunner/collections and select data file from      folder issapitestrunner/dataset.

# Issues with API observed so far

# API -> satellite/[id]/tles
1. Doesn't validate the format values for invalid data or blank values or invalid format passed in the query parameter and always returns 200 irrespective instead of 400
2. Doesn't validate the format of the satellite id and always returns 404 instead of 400
3. Accepts any query parameters in the url apart from the format query parameter instead of throwing 400
4. Accepts any random separator for query values like # instead of , and doesnt return 400 instead of 200
5. The documentation lacks the actual datatypes of the request and response attributes, their format and max/min length considerations and mandatory/optional response fields
    
# API -> satellite/[id]/positions
1. Doesn't return any error message for Invalid Unit format, values or multiple units passed nor returns 400
2. Doesn't return all the invalid timestamps in the error message when one or more invalid timestamps are returned
3. Doesn't validate the format of the satellite id and always returns 404 instead of 400
4. Accepts any query parameters in the url apart from the timestamps and units query parameter instead of throwing 400
5. Doesn't validate the range of timestamps values and hence returns 500 for very big timestamp value instead of 400
6. Accepts more than 10 timestamps even though it is supposed to accept only 10 timestamps in one call
7. Accepts any random separator for query values like # instead of , and doesnt return 400 instead of 200
8. Accepts more than one units in the units query parameter instead of 1 and only returns kilometers in those cases (units query parameter can be renamed to unit since it        accepts only one)
10. Accepts duplicates in timestamps query parameter and returns duplicate records instead of 1 unique record
11. Returns incorrect error message when timestamps is sent as arrays [1234,4567]
12. The documentation lacks the actual datatypes of the request and response attributes, their format and max/min length considerations and mandatory/optional response fields
13. Returns an array when we pass one timestamp and it has just one record. Ideally should return just one object.
   


