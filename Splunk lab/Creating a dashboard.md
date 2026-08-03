# Overview
This section demonstrates the creation of two different dashboards for Linux events.


For instance, this query searches for Linux events that correlate to failed logins, and each field is sorted in descending order.
<img width="1918" height="1042" alt="image" src="https://github.com/user-attachments/assets/28618d91-68c7-429f-aa9e-c01a16363386" />

With this panel I created, I can use the panel to help create a Dashboard
I also created a timeline that visually demonstrates the failed logins by top users with the timespan of 1 hour.
This was the SPL query used to generate a timeline of Failed logins within 1 hour
<img width="1605" height="298" alt="image" src="https://github.com/user-attachments/assets/bafdf013-9d6e-4cf7-bafe-b60827d9046b" />
And this is the graph that shows the events occured
<img width="1562" height="348" alt="image" src="https://github.com/user-attachments/assets/d528754c-3c31-4633-99a9-c1c0345e8dd7" />
Even though we've looked at failed logins, I searched for any successful logins to a user account by a remote host.
<img width="1605" height="661" alt="image" src="https://github.com/user-attachments/assets/263562ee-3520-48c4-99a7-a155bd3a3225" />
The query above is similar to the last query, except it searches for successful logins by the keyword **accepted**.
We can use this query to create a panel for successful logins by user
<img width="1605" height="825" alt="image" src="https://github.com/user-attachments/assets/e8ab52b6-0654-40cc-91ec-7492ec141213" />
Now I've created a basic dashboard for Linux events that show failed, and successful logins.
