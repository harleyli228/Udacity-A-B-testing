# Udacity A B testing
## Free Trail Screener
In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. 
- If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. 
- If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion and suggesting that the student might like to access the course materials for free. 
At this point, the student would have the option to continue enrolling in the free trial or access the course materials for free instead. This screenshot shows what the experiment looks like.

The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—without significantly reducing the number of students to continue past the free trial and eventually complete the course. 
- Reduce the number of students that leave the free trial 
- Not reduce the number of students pass free trail and complete the course
If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.

The unit of diversion is a cookie, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.
Experiment Design

## Metric Choice
- Invariant metrics
    - Number of cookies: That is, number of unique cookies to view the course overview page. (dmin=3000) 
      - unit of diversion
      - control and experiment groups should be the same
  -	Number of clicks: That is, number of unique cookies to click the "Start free trial" button (which happens before the free trial screener is trigger). (dmin=240)
      - before experiment  
  - Click-through-probability: That is, number of unique cookies to click the "Start free trial" button divided by number of unique cookies to view the course overview page. (dmin=0.01)  
      - before experiment 

-	Evaluation metrics
    -	Gross conversion: That is, number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the "Start free trial" button. (dmin= 0.01) 
        -	From click -> enroll free trial 
    -	Retention: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. (dmin=0.01)
        -	From enroll free trail -> past 14-day boundary
    -	Net conversion: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the "Start free trial" button. (dmin= 0.0075)
        -	From click -> past 14-day boundary
 
-	Udacity wants to increase the retention rate without reducing the net conversion rate
-	Gross conversion rate might decrease

## Measuring Standard Deviation

| Metrics          | Standard deviation |
| ------------- | ------------- |
| Gross conversion |    0.020230604     |
| Retention        |    0.054949012     |
| Net conversion   |    0.015601545     |

## Sizing
## Number of Samples vs. Power

| Metrics          | Calculator | Pageviews |
| ------------- | ------------- | --- |
| Gross conversion |    25835     | 645875 |
| Retention        |    78230     |4741212|
| Net conversion   |    27413	    |685325|

- Pageviews required is maximum of pageviews required for Gross Conversion, Retention, Net Conversion. Therefore, the required pageviews is 4741212.
- No need to use the Bonferroni correlation. The three metrics are correlated, using Bonferroni will make it too conservative.


## Duration vs. Exposure
### with 100% traffic diversion

| Metrics          | Duration |
| ------------- | ------------- |
| Gross conversion |    16     |
| Retention        |    119     |
| Net conversion   |    17	    |

### with 80% traffic diversion

| Metrics          | Duration |
| ------------- | ------------- |
| Gross conversion |    20     |
| Retention        |    148     |
| Net conversion   |    21	    |

## Experiment Analysis
### Sanity Checks
  
| Metrics |  P-observed | CI-lower|	CI-upper	|Sanity |
| ---------| ---- | ------------- |--|--|
|Number of cookies|	0.500639667|	0.49882039|	0.50117961|	PASS|
|Number of clicks on "start free trail"	|0.500467347	|0.4958845|	0.5041155|	PASS|
|Click-through-probability on "start free trail"|	-5.66271E-05|	-0.0012957|	0.00129568|	PASS|

## Result Analysis
### Effect Size Tests

| Metrics | 	m|	Lower|	Upper	|dmin	|Statistical|	Practical|
| ----|-----| ---- | -----|-------- |--|--|
|Gross conversion|	0.00856848	|-0.0291234|	-0.0119864|	0.01	|Yes|	Yes|
|Retention|	0.02299037|	0.00810444|0.05408517|	0.01|	Yes	|No|
|Net conversion	|0.0067309	|-0.0116046|	0.00185718|	0.0075|	No|	No|

### Sign Tests
	
|Number of successes	|Number of trails	|The two-tail P value |
| ---------| ---- | ------------- |
|Gross conversion|	4|	23|	0.0026|
|Retention|	13	|23	|0.6776|
|Net conversion	|10|	23|	0.6776|

## Summary
The Bonferonni correction is a method for controlling for type I errors (false positives) when using multiple metrics in which relevance of ANY of the metrics matches the hypothesis. In our case in which ALL metrics must be relevant to launch, the risk of type II errors (false negatives) increases as the number of metrics increases, so it stands to reason that controlling for false positives is not consistent with our acceptance criteria.

Hypothesis:
-	Increase the retention rate 
-	Not reduce the net conversion rate
-	Gross conversion rate might decrease

Discrepancies between the effect size hypothesis tests and the sign tests:
-	Gross conversion has practical significance, statistical significance and past the sign test
-	Retention rate is statistically significant but not practically significant. It did not pass the sign test
-	Net conversion rate is neither statistically significant nor practically significant

## Recommendation

I would not recommend launching the change for the following reasons:
- We only had Gross conversion that was both statistically significant and practically significant. However, the change is negative.
- The change in retention rate is positive, but it is not practically significant.
- There is no significant effect in Net conversion rate.
