# AWS Connect Project
- Designed and implemented an automated call center system using cutting-edge AWS services like Amazon Connect, Lex, Lambda, and Contact Lens to optimize call flow and improve customer experience
- Established a robust data pipeline for visualizing customer trace records (CTR) data from Connect calls on Quicksight, leveraging powerful tools like Firehose, Glue, Athena, and S3 to collect, process, and store data 
- Explored sentiment analysis on call recordings using Contact Lens, providing valuable insights to identify areas for improvement in customer service

Quicksight Flow:

- The (CTR)Contact Trace Record(a json file which provides detailed information about the interactions between customers and agents in a contact center in terms of customer's phone number or chat ID, the date and time of the contact, the agent who handled the interaction, etc.) is streamed into an s3 bucket named connectfirehoseoutputbucket from a Kinesis Firehose
- Then a glue crawler(named firehosecrawler) is made to crawl on the ctr json file in order to identify the schema of the data, the output of this is stored in another s3 bucket
- Going forward we query the data into a desired tablular format using Athena
- The table is then imorted into a glue notebook in order to be filtered for desired results, and the output from the ETL job is stored in an s3 bucket
- Quicksight is connect directly to this s3 bucket(with a manifest json permission file for access to the data) and data is visualized

AWS Flowchart for Quicksight Analytics:

![image](https://user-images.githubusercontent.com/62932933/219936837-e79e24b2-6870-4dbf-bc79-9c9a3055ee4b.png)

Quicksight Report:

![image](https://user-images.githubusercontent.com/62932933/219972278-7ea0108f-cd00-4cc7-96da-18a1c77c15bb.png)

Using Contact Lens for sentiment analysis:

- Make sure that the contact lens option is enabled in the analytics panel within your connect instance

![image](https://user-images.githubusercontent.com/62932933/221545982-7cd1db1a-40e6-4339-8e64-fbf0f7c3c0da.png)

- Then go to your contact flow and add the "Set recording and analytics behavior" block at the beginning of your flow, with all the settings as shown in the following gif:
 
![ezgif com-video-to-gif](https://user-images.githubusercontent.com/62932933/221545650-fcc8b46c-29ab-4ab5-97d8-76d116728775.gif)

- Lastly go to the Analytics and Optimization tab to access the call recordings and their summary

