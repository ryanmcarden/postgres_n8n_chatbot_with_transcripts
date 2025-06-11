# postgres_n8n_chatbot_with_transcripts
a n8n workflow for a n8n chatbot that emails the end users new chat transcripts hourly.

## 👨‍🎤 Chatbot Setup
1. setup Postgres Db
2. setup n8n credential for the Postgres Db you setup in step 1
3. setup basic n8n Chatbot workflow 
4. connect Postgres Memory node to AI Agent and connect it to your db with the credential setup in step 2
5. click the open chat button in your n8n workflow and do a test chat with the AI agent. If your node is connected correctly to your Db, the test chat will create a table called "n8n_chat_histories"
6. Open your database in pgAdmin (or something similar) and add a column named "date_time". 
6.5 make sure and give your new "date_time" column the datatype of "timestamp without timezone" and set the default constraint to "CURRENT_TIMESTAMP". This gives your chat history timestamps.
7. See the sub-workflow below that sends the email transcripts.
8. Activate workflow

## 👨‍🎤 Email Sub-Workflow Setup
9. connect your Postgres Db credential that you setup in setup 2 with the below Postgres nodes.
10. if you didn't change any of the Db column names, you shouldn't have to modify any of the postgres queries or other code that I wrote
11. setup a Gmail credential and add it to the Gmail node. You can use any email provider of your choice. 
12. the two variables available for your email message node will be: {{ $json.data.session_id }} and {{ $json.emailBody }} 
13. you can change how often this tool runs via line 4 of the query located in the "Lookup Last 60 Minutes Chat Session Ids" node
14. activate workflow

## Notes
this workflow was created on a locally hosted version of n8n which was installed via Node.js  
email ryan@ryancarden.com if you find any bugs or have suggestions
