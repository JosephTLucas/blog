# HackThisAI: easy_credit_check

This is a walkthrough of the easy [HackThisAI](https://github.com/JosephTLucas/HackThisAI) challenge: easy_credit_check.

We see the instructions here.  
![instructions](img/instructions.JPG)

As listed on the main README, the docker component of this is because it's a prototype. There'll be a much more straightforward process when the CTF is a web service.

We see from the instructions that we need to make a small change to `Mall_Customers.csv`, rename the file to `tamper.csv` and see if we can get a 19 year old making $15k approved.

Let's look at the data:  
![data_sample](img/data_sample.JPG)

Okay, so we see that each customer has an `ID`, "`Genre`" (looks like gender), `Age`, `Income`, and `Spending Score`. From the prompt, we know that we want to get our spending score above 90. What is it now? Let's just `cp Mall_Customers.csv tamper.csv` and see what our score is right now.  
![status_quo](img/status_quo.JPG)

Okay, so it doesn't tell us our score, but we can assume it's below 90. I noticed that the first record in the dataset applies directly to us `Age:19, Income: 15`. We're assuming this is training data... maybe a supervised regression problem. This is a data poisoning attack. If we change this record to what we want, maybe that'll reflect in the trained model.

![first_record](img/first_record.JPG)

Now let's try again.

![flagrant](img/flagrant.JPG)

Oh man, it looks like there is some kind of data integrity check... Let's try again, but maybe this time we'll just add a record.

![1tail](img/1tail.JPG)

Hmm... we still don't qualify. We can see that `100` seems to be the max `Score`. Maybe we should increase from `90` to `100` (give ourselves some margin)? Nope, still doesn't work.

I wonder how well they do data validation?

![flag](img/flag.JPG)

Apprently poorly! It looks like they don't bound/scale the target variable (`Score`) on a reasonable range. By increasing this an absurd amount, we're able to change the decision boundary and win!
