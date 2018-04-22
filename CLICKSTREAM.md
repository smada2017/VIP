# VIP Clickstream Data Process

## About

This is our documentation for our work on clickstream data this semester. Our main objective this semester was to replicate the project that we conducted with the CS1301 data previously from last semester by creating a similar model, but also splitting up our data between audit and verified. So first we did some basic SQL pulls from our data to get information about students ids, whether they were verified or audit, and scores throughout the course on every quiz and assignments. The information on grading consisted of 10 weekly grades, 2 midterm quizzes, final course project, and a final quiz. 

## Initial Model

Using the averages for the first three weeks and midterm 1 quiz scores we created a model to organize students into four different categories. These categories were High Achieving, Above Average, Average, and Failing. The score ranges for these categories respectively were 100-90, 90-80, 80-65, and 65-0. We then organized the students first into whether they were audit or verified, and then separated them into their respective categories depending on the averages of the first three weeks and midterm 1 quiz scores. Then we analyzed the growth of the four categories growth over the course, and we specifically had checkpoints at the midterm quiz 2, and the final grade. 

## Expanding the Model

To really replicate the previous semester's work we realized that we should involve clickstream data into our model to have a better parameter to analyze growth. So since there was a large amount of clickstream data that was very variant in the types of information it had we decided to utilize a noSQL database, MongoDB, to go through the data and parse for the information we wanted. However, we ran into the obstacle of running MongoDB on our computers and this lead us to unfortunately not be able to complete our analysis of the clickstream data. We suspect that there is an issue with the security measures on the newest version of iOS that prevents proper installation of MongoDB. 

## Future Steps

Our main roadblock of installing MongoDB did not prevent us from planning on how to actually complete the analysis. The remainder of this document is the code and steps that need to be completed once MongoDB is running on our systems.

1. First, find the distinct events that the click stream data has. Look for anything that is related to videos or other parameters that could provide insights on effort or performance of students in the course. Write this line into your terminal after starting MongoDB and importing the clickstream data into your database:

```
db.logData.distinct("event");
```

2. Then use the following code to find the data that is specifcally relevant to ISYE and has the distinct event that you are looking for:

```
var criteria = {}, 
condition = [ {"event.course_id": course id for ISYE}, {"event": video} ]; 
if (query.name !== "") { 
criteria["$and"] = condition; 
} else { 
criteria["$or"] = condition; 
}

db.test.find(criteria);
```

3. You can then export your database results (write the previous code into a javascript file) using the mongoexport function:

```
script.js >> test.csv
```

4. Use excel or tableau to parse data and create visualizations and conduct any other analyses that might provide insights. 
