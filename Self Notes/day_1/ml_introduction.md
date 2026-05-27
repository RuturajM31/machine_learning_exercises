# Machine Learning — Day 1 Study Guide

## Very Simple, Visual Explanation for a Complete Beginner

### Focus: Classification, Regression, Linear Regression, Loss, and Gradient Descent

---

## How to Read This Guide

Do **not** try to memorize formulas first.

First understand the story:

```text
Old data  →  Machine finds pattern  →  Machine predicts new result
```

That is the heart of Machine Learning.

In your Data Analyst / BI / Digital Marketing / Inventory profile, ML is useful for questions like:

```text
Can we predict future conversions?
Can we predict sales demand?
Can we identify high-risk customers?
Can we classify campaigns as good or bad?
Can we detect slow-moving inventory?
```

---

# 1. Machine Learning in One Simple Idea

Machine Learning means:

```text
The computer learns from examples instead of only following fixed human-written rules.
```

## Normal Programming

In normal programming, you write the rule yourself.

```text
Human writes rule  →  Computer follows rule
```

Example:

```text
If CTR > 5%, campaign = Good
Else campaign = Bad
```

Problem:

Real business data is not that simple.

A campaign can have high CTR but low conversions.
A campaign can have low CTR but very good revenue.
A campaign can perform differently by device, country, product, or season.

---

## Machine Learning

In Machine Learning, you give examples to the machine.

```text
Human gives past examples  →  Machine learns pattern  →  Machine predicts
```

Example:

| Campaign |  CTR |   CPC | Budget | Device  | Conversions |
| -------- | ---: | ----: | -----: | ------- | ----------: |
| A        | 4.5% | €0.80 |   €500 | Mobile  |          35 |
| B        | 2.1% | €1.50 |   €300 | Desktop |           8 |
| C        | 6.2% | €0.60 |   €700 | Mobile  |          70 |

The model may learn:

```text
High CTR + low CPC + good budget + mobile traffic often gives more conversions.
```

Then for a new campaign:

|  CTR |   CPC | Budget | Device | Predicted Conversions |
| ---: | ----: | -----: | ------ | --------------------: |
| 5.0% | €0.70 |   €600 | Mobile |                    50 |

---

# 2. Human Intelligence vs Machine Learning

Your slides show simple human examples:

```text
What should I eat?
What should I wear?
Is this a cat?
What number is this?
What grade will I get if I study 4 hours?
```

Humans use information and past experience:

```text
Information  →  Brain  →  Decision / Prediction
```

Machine Learning uses data and a model:

```text
Data  →  Model  →  Prediction
```

## Visual Comparison

```text
Human:
Weather + past experience  →  Brain  →  Wear jacket

Machine:
Weather data + past clothing examples  →  Model  →  Predict jacket
```

---

# 3. Important ML Words

| Word              | Very Simple Meaning              | Example from Your Profile               |
| ----------------- | -------------------------------- | --------------------------------------- |
| Dataset           | A table of data                  | Past Google Ads campaigns               |
| Row / Observation | One record                       | One campaign, one product, one customer |
| Features          | Input columns                    | clicks, CPC, device, stock, season      |
| Label / Target    | Column we want to predict        | conversions, revenue, demand, churn     |
| Model             | The trained machine brain        | conversion prediction model             |
| Training          | Teaching the model with old data | use historical campaign data            |
| Prediction        | Model's answer                   | expected conversions next week          |
| Error / Loss      | How wrong the prediction is      | predicted 50, actual 40                 |

---

# 4. Features and Label

This is one of the most important concepts.

```text
Features = input information
Label / Target = answer we want to predict
```

## Simple Study Example

| Hours Studied | Points |
| ------------: | -----: |
|             1 |      2 |
|             2 |      4 |
|             3 |      6 |

Here:

```text
Feature = Hours Studied
Label = Points
```

The machine learns:

```text
Hours studied affects points.
```

---

## Digital Marketing Example

| Impressions | Clicks |   CPC | Device  | Conversions |
| ----------: | -----: | ----: | ------- | ----------: |
|      10,000 |    500 | €0.80 | Mobile  |          30 |
|       5,000 |    100 | €1.50 | Desktop |           5 |
|      20,000 |    900 | €0.60 | Mobile  |          75 |

Here:

```text
Features = Impressions, Clicks, CPC, Device
Label = Conversions
```

ML question:

```text
Can we predict conversions using campaign information?
```

---

## Inventory Example

| Product Category | Current Stock | Past Sales | Season | Supplier Lead Time | Future Demand |
| ---------------- | ------------: | ---------: | ------ | -----------------: | ------------: |
| Brakes           |           200 |         50 | Summer |            10 days |            70 |
| Filters          |            50 |         10 | Winter |            20 days |            15 |
| Wheels           |           500 |        120 | Summer |             7 days |           150 |

Here:

```text
Features = category, stock, past sales, season, lead time
Label = future demand
```

ML question:

```text
Can we predict how many units will be needed next month?
```

---

# 5. Training Data and Test Data

## Training Data

Training data is used to teach the model.

```text
Training data = examples the model learns from
```

## Test Data

Test data is used to check if the model learned properly.

```text
Test data = new examples the model has not seen before
```

## Visual

```text
Historical data
      |
      v
+----------------------+----------------------+
| Training Data        | Test Data            |
| Teach the model      | Check the model      |
| Example: Jan-Nov     | Example: December    |
+----------------------+----------------------+
```

Why do we test?

Because the model should not only memorize old data.
It should work on new business data.

---

# 6. Supervised Learning

Your Day 1 slides mainly talk about **supervised learning**.

## Very Simple Definition

Supervised learning means:

```text
The model learns from data where the correct answer is already known.
```

The correct answer is called:

```text
Label / Target / Actual value
```

---

## Example

| Hours Studied | Actual Points |
| ------------: | ------------: |
|             1 |             2 |
|             2 |             4 |
|             3 |             6 |

The model sees both:

```text
Input = hours studied
Correct answer = points
```

So the machine is being “supervised” because the answer is already provided.

---

## Business Example

| Clicks | Cost | Device  | Actual Conversions |
| -----: | ---: | ------- | -----------------: |
|    500 | €200 | Mobile  |                 20 |
|    100 |  €80 | Desktop |                  2 |
|    800 | €300 | Mobile  |                 45 |

The model sees:

```text
Input = clicks, cost, device
Correct answer = conversions
```

Then it learns:

```text
Which campaign patterns usually lead to more conversions?
```

---

# 7. Classification vs Regression — The Most Important Difference

Your slides compare **classification** and **regression**.

This is one of the biggest beginner topics in ML.

## The Simple Rule

```text
Classification = predict a category / class
Regression = predict a number
```

## Visual Memory Trick

```text
Question: What type of answer do I want?

             +----------------------+
             | Model Prediction     |
             +----------------------+
                       |
         +-------------+-------------+
         |                           |
         v                           v
  Category / Class              Number / Amount
  = Classification              = Regression
```

---

# 8. Classification — Explained Slowly

## 8.1 What Is Classification?

Classification means:

```text
The model puts something into a category.
```

The answer is not a quantity.

The answer is a label such as:

```text
Yes / No
Good / Bad
Spam / Not Spam
Cat / Dog
High Risk / Low Risk
Fast-moving / Slow-moving / Dead stock
```

---

## 8.2 Very Simple Human Example

You see an animal.

You ask:

```text
Is this a cat or a dog?
```

Possible answers:

```text
Cat
Dog
```

This is classification because the answer is a category.

```text
Image  →  Model  →  Cat
```

This matches your slide where the model looks at a picture and predicts “cat”.

---

## 8.3 Binary Classification

Binary means two options.

```text
Binary Classification = classification with only two possible answers
```

Examples:

| Problem                 | Possible Answers            |
| ----------------------- | --------------------------- |
| Will customer churn?    | Yes / No                    |
| Will lead convert?      | Yes / No                    |
| Is email spam?          | Spam / Not Spam             |
| Is campaign profitable? | Profitable / Not Profitable |
| Is stockout risk high?  | High Risk / Low Risk        |

---

## 8.4 Multiclass Classification

Multiclass means more than two possible options.

```text
Multiclass Classification = classification with 3 or more possible answers
```

Examples:

| Problem                        | Possible Answers                           |
| ------------------------------ | ------------------------------------------ |
| What animal is in the picture? | Cat / Dog / Horse / Bird                   |
| What type of campaign is it?   | Excellent / Average / Poor                 |
| What type of product movement? | Fast-moving / Slow-moving / Dead stock     |
| What support ticket category?  | Billing / Technical / Delivery / Complaint |

Your image-classification slide is multiclass classification because the model can choose from many object classes.

---

## 8.5 Classification in Digital Marketing

### Example: Lead Conversion Prediction

Business question:

```text
Will this website visitor become a lead?
```

Possible answers:

```text
Yes
No
```

So this is:

```text
Classification
```

Dataset:

| Source     | Device  | Pages Visited | Session Duration | Converted? |
| ---------- | ------- | ------------: | ---------------: | ---------- |
| Google Ads | Mobile  |             5 |          180 sec | Yes        |
| Organic    | Desktop |             1 |           20 sec | No         |
| LinkedIn   | Desktop |             7 |          300 sec | Yes        |

Here:

```text
Features = source, device, pages visited, session duration
Label = converted yes/no
```

Visual:

```text
Visitor data  →  Model  →  Yes / No
```

---

## 8.6 Classification in Inventory Analytics

Business question:

```text
Is this product fast-moving, slow-moving, or dead stock?
```

Possible answers:

```text
Fast-moving
Slow-moving
Dead stock
```

So this is:

```text
Multiclass Classification
```

Dataset:

| Product | Stock Age | Monthly Sales | Stock Quantity | Product Class |
| ------- | --------: | ------------: | -------------: | ------------- |
| A       |   10 days |           500 |            100 | Fast-moving   |
| B       |  180 days |             5 |            300 | Slow-moving   |
| C       |  365 days |             0 |           1000 | Dead stock    |

Visual:

```text
Inventory data  →  Model  →  Fast / Slow / Dead stock
```

---

## 8.7 Classification Often Gives Probabilities

A classification model often does not only say:

```text
Yes
```

It may first calculate probabilities:

```text
Probability of Yes = 82%
Probability of No = 18%
```

Then it chooses the bigger one:

```text
Final prediction = Yes
```

### Marketing Example

```text
Lead conversion probability = 78%
```

Business use:

```text
Sales team should call this lead first.
```

---

## 8.8 Classification Visual: Decision Boundary

Imagine each dot is a lead.

```text
High chance leads = X
Low chance leads  = O
```

```text
Engagement
   |
10 |        X   X   X
 9 |      X   X
 8 |    X
 7 |----------------------  ← model's separation line
 6 |        O
 5 |    O      O
 4 | O    O
 3 | O
   +-------------------------
        Low           High
            Website Activity
```

The line separates two classes:

```text
Above line = likely to convert
Below line = unlikely to convert
```

This line is called a **decision boundary**.

Do not worry about the technical term now. Just remember:

```text
Classification separates data into groups.
```

---

## 8.9 How to Recognize Classification Quickly

Ask yourself:

```text
Is the answer a name, group, or category?
```

If yes:

```text
Classification
```

Examples:

| Question                | Output             | Type           |
| ----------------------- | ------------------ | -------------- |
| Will the customer buy?  | Yes / No           | Classification |
| Is the campaign good?   | Good / Bad         | Classification |
| Which channel is best?  | SEO / SEA / Social | Classification |
| Is product slow-moving? | Yes / No           | Classification |

---

# 9. Regression — Explained Slowly

## 9.1 What Is Regression?

Regression means:

```text
The model predicts a number.
```

The answer is a quantity, amount, score, price, demand, revenue, or count.

Examples:

```text
45 conversions
€20,000 revenue
300 units demand
12.5% churn probability score
8 points
€450,000 house price
```

---

## 9.2 Simple Human Example

Question:

```text
If I study 4 hours, how many points will I get?
```

Possible answer:

```text
8 points
```

This is regression because the answer is a number.

---

## 9.3 Regression in Digital Marketing

Business question:

```text
How many conversions will this campaign generate?
```

Possible answer:

```text
52 conversions
```

So this is:

```text
Regression
```

Dataset:

| Impressions | Clicks |   CPC | Budget | Conversions |
| ----------: | -----: | ----: | -----: | ----------: |
|      10,000 |    500 | €0.80 |   €400 |          30 |
|      20,000 |    900 | €0.60 |   €700 |          75 |
|       5,000 |    100 | €1.50 |   €200 |           5 |

Here:

```text
Features = impressions, clicks, CPC, budget
Label = conversions
```

Visual:

```text
Campaign data  →  Model  →  52 conversions
```

---

## 9.4 Regression in Inventory Analytics

Business question:

```text
How many units will we need next month?
```

Possible answer:

```text
850 units
```

So this is:

```text
Regression
```

Dataset:

| Past Sales | Current Stock | Season | Lead Time | Future Demand |
| ---------: | ------------: | ------ | --------: | ------------: |
|        500 |           200 | Summer |        10 |           650 |
|        100 |            50 | Winter |        20 |           120 |
|        900 |           400 | Summer |         7 |          1000 |

Visual:

```text
Inventory data  →  Model  →  850 units demand
```

---

## 9.5 Regression Visual: Best-Fit Line

Imagine this is campaign budget and conversions.

```text
Conversions
   |
80 |                         *
70 |                    *
60 |                *
50 |           *
40 |       *
30 |    *
20 | *
   +--------------------------------
       100  200  300  400  500
              Campaign Budget
```

Regression tries to draw the best line:

```text
Conversions
   |
80 |                         *
70 |                    *
60 |                *
50 |           *
40 |       *
30 |    *
20 | *
   |--------------------------------  ← best-fit line
   +--------------------------------
       100  200  300  400  500
              Campaign Budget
```

Then for a new budget, the model uses the line to predict conversions.

---

## 9.6 How to Recognize Regression Quickly

Ask yourself:

```text
Is the answer a number?
```

If yes:

```text
Regression
```

Examples:

| Question                  |   Output | Type       |
| ------------------------- | -------: | ---------- |
| How many conversions?     |       52 | Regression |
| How much revenue?         |  €75,000 | Regression |
| How many units sold?      |      850 | Regression |
| What will CPC be?         |    €0.82 | Regression |
| What will house price be? | €450,000 | Regression |

---

# 10. Classification vs Regression — Side-by-Side

| Point             | Classification              | Regression             |
| ----------------- | --------------------------- | ---------------------- |
| Predicts          | Category / class            | Number                 |
| Output example    | Yes / No                    | 52 conversions         |
| Marketing example | Will lead convert?          | How many conversions?  |
| Inventory example | Fast-moving or slow-moving? | How many units needed? |
| Model output      | Class label                 | Numeric value          |
| Simple memory     | “Which group?”              | “How much?”            |

---

## Visual Decision Tree

```text
Start
  |
  v
What do you want to predict?
  |
  +-- A category? ------------------> Classification
  |       Examples: Yes/No, Cat/Dog, Good/Bad
  |
  +-- A number? --------------------> Regression
          Examples: revenue, demand, conversions, price
```

---

## Practice: Classification or Regression?

| Problem                                     | Answer         | Why?               |
| ------------------------------------------- | -------------- | ------------------ |
| Predict if a lead will convert              | Classification | answer is Yes / No |
| Predict number of conversions               | Regression     | answer is a number |
| Predict if a product is slow-moving         | Classification | answer is category |
| Predict future stock demand                 | Regression     | answer is number   |
| Predict campaign quality as high/medium/low | Classification | answer is class    |
| Predict monthly revenue                     | Regression     | answer is amount   |

---

# 11. Linear Regression — Explained Very Slowly

Linear regression is a type of regression.

Remember:

```text
Regression = predict a number
Linear Regression = predict a number using a straight-line relationship
```

---

## 11.1 Where Linear Regression Fits

```text
Machine Learning
   |
   v
Supervised Learning
   |
   v
Regression
   |
   v
Linear Regression
```

So linear regression is not separate from regression.

It is one method inside regression.

---

## 11.2 What Does “Linear” Mean?

Linear means:

```text
Straight-line relationship
```

Example:

```text
When x increases, y also increases in a steady way.
```

Your slide example:

| Hours Studied | Points |
| ------------: | -----: |
|             1 |      2 |
|             2 |      4 |
|             3 |      6 |
|             4 |      ? |

Look carefully:

```text
1 hour  → 2 points
2 hours → 4 points
3 hours → 6 points
```

Each extra hour adds 2 points.

So:

```text
4 hours → 8 points
```

---

## 11.3 Visual Pattern

```text
Hours:   1      2      3      4
Points:  2      4      6      ?

Pattern:
+1 hour means +2 points

So:
4 hours = 8 points
```

---

## 11.4 Plotting the Points

The data points are:

```text
(1, 2)
(2, 4)
(3, 6)
```

Visual:

```text
Points
  |
8 |                         ?
7 |
6 |                  *
5 |
4 |           *
3 |
2 |    *
1 |
  +-----------------------------
       1      2      3      4
              Hours
```

The points form a straight-line pattern.

So for 4 hours, the next point should be 8.

```text
Points
  |
8 |                         *  ← prediction
7 |
6 |                  *
5 |
4 |           *
3 |
2 |    *
1 |
  +-----------------------------
       1      2      3      4
              Hours
```

---

## 11.5 Linear Regression Formula

Your slide uses this simple formula:

```text
ŷ = x × w
```

Read it like this:

```text
Predicted value = input × weight
```

| Symbol | Meaning             | In Study Example |
| ------ | ------------------- | ---------------- |
| x      | input               | hours studied    |
| y      | actual answer       | actual points    |
| ŷ      | predicted answer    | predicted points |
| w      | weight / multiplier | 2                |

---

## 11.6 What Is w?

`w` is the multiplier.

In the study example:

```text
Points = Hours × 2
```

So:

```text
w = 2
```

If:

```text
x = 4
w = 2
```

Then:

```text
ŷ = x × w
ŷ = 4 × 2
ŷ = 8
```

---

## 11.7 Why Does the Machine Need to Learn w?

Because the machine does not know the correct multiplier at the beginning.

It tries different values of `w`.

|  w | Prediction for x=1 | Prediction for x=2 | Prediction for x=3 | Good or Bad?  |
| -: | -----------------: | -----------------: | -----------------: | ------------- |
|  1 |                  1 |                  2 |                  3 | too low       |
|  2 |                  2 |                  4 |                  6 | perfect       |
|  3 |                  3 |                  6 |                  9 | too high      |
|  4 |                  4 |                  8 |                 12 | much too high |

The best `w` is:

```text
w = 2
```

Because it gives correct predictions for the training data.

---

## 11.8 Linear Regression with Bias b

Later, you will see a fuller formula:

```text
ŷ = w × x + b
```

Here:

```text
w = slope / weight
b = bias / intercept
```

Very simple meaning:

```text
w decides how steep the line is.
b decides where the line starts.
```

---

## 11.9 Visual: w and b

```text
ŷ = w × x + b
```

Imagine a line:

```text
Points
  |
8 |                         /
7 |                       /
6 |                     /
5 |                   /
4 |                 /
3 |               /
2 |-------------/----------------  ← b controls starting position
1 |
  +-----------------------------
       1      2      3      4
              x
```

* If `w` changes, the line becomes steeper or flatter.
* If `b` changes, the line moves up or down.

---

## 11.10 Business Example: Ad Spend and Conversions

Suppose you have:

| Ad Spend | Conversions |
| -------: | ----------: |
|     €100 |          10 |
|     €200 |          20 |
|     €300 |          30 |
|     €400 |           ? |

Look at the pattern:

```text
€100 → 10 conversions
€200 → 20 conversions
€300 → 30 conversions
```

Every extra €100 gives 10 extra conversions.

So:

```text
€400 → 40 conversions
```

Relationship:

```text
Conversions = Ad Spend × 0.1
```

Here:

```text
x = Ad Spend
w = 0.1
ŷ = predicted conversions
```

For €400:

```text
ŷ = 400 × 0.1
ŷ = 40
```

---

## 11.11 Real Marketing Data Is Not Perfect

Real data may look like this:

| Ad Spend | Actual Conversions |
| -------: | -----------------: |
|     €100 |                  8 |
|     €200 |                 23 |
|     €300 |                 27 |
|     €400 |                 41 |

This is not perfect.

Why?

Because real conversions depend on many things:

```text
ad copy
landing page
device
country
season
competition
audience quality
product price
brand trust
```

Linear regression does not find a perfect rule.

It finds the best approximate line.

```text
Best approximate line = line with the smallest overall error
```

---

## 11.12 Visual: Best Approximate Line

```text
Conversions
  |
45 |                         *
40 |                    ----/
35 |                ----
30 |             *
25 |         ----
20 |      *
15 |   ----
10 | *
  +--------------------------------
      100    200    300    400
              Ad Spend
```

Some points are above the line.
Some points are below the line.
The model chooses the line that is overall closest to all points.

---

# 12. Actual Value vs Predicted Value

During training, the model predicts something.

Then we compare prediction with the real answer.

```text
Actual value = real answer
Predicted value = model answer
```

## Example

| Hours | Actual Points | Predicted Points |
| ----: | ------------: | ---------------: |
|     1 |             2 |                3 |
|     2 |             4 |                6 |
|     3 |             6 |                9 |

Here, the model used:

```text
w = 3
```

So prediction was:

```text
ŷ = x × 3
```

But actual pattern is:

```text
y = x × 2
```

So the model is wrong.

---

# 13. Error / Loss

## Simple Definition

Loss means:

```text
How wrong the model is.
```

Small loss:

```text
Good model
```

Big loss:

```text
Bad model
```

---

## Example

Actual conversions:

```text
40
```

Predicted conversions:

```text
35
```

Error:

```text
40 - 35 = 5
```

The model was wrong by 5 conversions.

---

# 14. MSE — Mean Squared Error

Your slide uses **MSE**.

MSE means:

```text
Mean Squared Error
```

Very simple meaning:

```text
Average squared mistake of the model
```

---

## 14.1 Why Square the Error?

Because errors can be positive or negative.

Example:

```text
Prediction 1 error = +5
Prediction 2 error = -5
```

If we simply add:

```text
+5 + -5 = 0
```

That looks like no error, but actually both predictions were wrong.

So we square the errors:

```text
(+5)² = 25
(-5)² = 25
```

Now both mistakes count.

---

## 14.2 MSE Steps

For each row:

```text
1. Prediction - Actual
2. Square the difference
3. Add all squared errors
4. Divide by number of rows
```

---

## 14.3 MSE Example: Bad w

Suppose:

```text
w = 3
```

Actual data:

| Hours | Actual y | Prediction ŷ | Error ŷ - y | Squared Error |
| ----: | -------: | -----------: | ----------: | ------------: |
|     1 |        2 |            3 |           1 |             1 |
|     2 |        4 |            6 |           2 |             4 |
|     3 |        6 |            9 |           3 |             9 |

Total squared error:

```text
1 + 4 + 9 = 14
```

Average:

```text
14 ÷ 3 = 4.67
```

So:

```text
MSE = 4.67
```

---

## 14.4 MSE Example: Perfect w

Suppose:

```text
w = 2
```

| Hours | Actual y | Prediction ŷ | Error | Squared Error |
| ----: | -------: | -----------: | ----: | ------------: |
|     1 |        2 |            2 |     0 |             0 |
|     2 |        4 |            4 |     0 |             0 |
|     3 |        6 |            6 |     0 |             0 |

Total squared error:

```text
0 + 0 + 0 = 0
```

Average:

```text
0 ÷ 3 = 0
```

So:

```text
MSE = 0
```

This is perfect for this small example.

---

# 15. What Is Training Actually Doing?

Training means:

```text
Find the best model parameters so the loss becomes as small as possible.
```

In the simple slide example, the only parameter is:

```text
w
```

The model tries different values:

|  w |  MSE | Meaning     |
| -: | ---: | ----------- |
|  0 | 18.7 | very bad    |
|  1 |  4.7 | still wrong |
|  2 |    0 | perfect     |
|  3 |  4.7 | still wrong |
|  4 | 18.7 | very bad    |

Best value:

```text
w = 2
```

Because loss is lowest.

---

## Visual: Loss Curve

```text
Loss / MSE
  |
20 | *                         *
18 |   *                     *
16 |
14 |
12 |
10 |
 8 |
 6 |        *           *
 4 |
 2 |
 0 |              *
  +--------------------------------
       0      1      2      3      4
                    w
```

The lowest point is at:

```text
w = 2
```

Training tries to reach this lowest point.

---

# 16. Gradient Descent — Explained Simply

Gradient descent is a method to find the best value of `w`.

## Very Simple Definition

Gradient descent means:

```text
Move step by step in the direction where error becomes smaller.
```

---

## Hill Example

Imagine you are standing on a hill.

Your goal:

```text
Reach the lowest point of the valley.
```

You do this:

```text
1. Look which direction goes down.
2. Take a small step downward.
3. Again check direction.
4. Take another step.
5. Continue until you reach the bottom.
```

---

## ML Translation

| Hill Example        | ML Meaning       |
| ------------------- | ---------------- |
| Height of hill      | Loss / error     |
| Position on hill    | Weight w         |
| Lowest valley point | Best w           |
| Step size           | Learning rate    |
| Walking downhill    | Gradient descent |

---

## Visual

```text
Loss
  |
  |       start
  |         ●
  |        /
  |      ●
  |     /
  |   ●
  |  /
  |●  lowest loss
  +-------------------
          w
```

The model moves from high loss to low loss.

---

# 17. Learning Rate

Learning rate controls step size.

It is usually written as:

```text
α
```

## Simple Meaning

```text
Learning rate = how big a step the model takes while learning
```

---

## Too Small Learning Rate

```text
Tiny steps
Very slow learning
```

Visual:

```text
●-●-●-●-●-●-●-●-●
```

Stable but slow.

---

## Too Big Learning Rate

```text
Huge jumps
May miss the best point
```

Visual:

```text
● -------- ● -------- ●
```

Fast but unstable.

---

## Good Learning Rate

```text
Medium steps
Moves steadily toward the best point
```

Visual:

```text
● ---- ● --- ● -- ● - ●
```

---

# 18. Full Day 1 ML Process

```text
1. Collect historical data
        ↓
2. Choose features and label
        ↓
3. Split into training and test data
        ↓
4. Choose model
        ↓
5. Train model
        ↓
6. Model predicts
        ↓
7. Compare prediction with actual value
        ↓
8. Calculate loss
        ↓
9. Adjust model parameters
        ↓
10. Repeat until loss is small
        ↓
11. Use trained model on new data
```

---

# 19. Same Process for Your Digital Marketing Profile

```text
1. Collect old campaign data
        ↓
2. Features: clicks, CPC, CTR, budget, device, country
        ↓
3. Label: conversions
        ↓
4. Train model on old campaigns
        ↓
5. Model predicts conversions for new campaign
        ↓
6. Compare predicted conversions with actual conversions
        ↓
7. Calculate error
        ↓
8. Improve model
        ↓
9. Use model for future budget planning
```

---

# 20. Same Process for Your Inventory Profile

```text
1. Collect old inventory and sales data
        ↓
2. Features: stock, past sales, season, lead time, category
        ↓
3. Label: future demand
        ↓
4. Train model
        ↓
5. Predict demand
        ↓
6. Compare prediction with actual demand
        ↓
7. Reduce error
        ↓
8. Use model for stock planning
```

---

# 21. Super Important Comparison Table

| Concept             | Simple Meaning             | Your Profile Example                  |
| ------------------- | -------------------------- | ------------------------------------- |
| ML                  | Learn pattern from data    | learn what drives conversions         |
| Supervised learning | learn with correct answers | campaign data with actual conversions |
| Feature             | input column               | clicks, CPC, device                   |
| Label               | answer column              | conversions                           |
| Classification      | predict category           | lead converts: yes/no                 |
| Regression          | predict number             | number of conversions                 |
| Linear regression   | predict number using line  | ad spend → conversions                |
| Prediction          | model answer               | 52 conversions                        |
| Actual value        | real answer                | actual 48 conversions                 |
| Error               | difference                 | wrong by 4 conversions                |
| Loss                | overall wrongness          | average mistake                       |
| MSE                 | average squared error      | model performance metric              |
| Gradient descent    | step-by-step improvement   | adjust w to reduce error              |
| Learning rate       | step size                  | small/large update                    |

---

# 22. Common Beginner Confusions

## Confusion 1: Is classification also prediction?

Yes.

Both classification and regression are prediction tasks.

Difference:

```text
Classification predicts category.
Regression predicts number.
```

---

## Confusion 2: Is linear regression the same as regression?

No.

Regression is the bigger family.

Linear regression is one specific type of regression.

```text
Regression
   ├── Linear Regression
   ├── Polynomial Regression
   ├── Decision Tree Regression
   ├── Random Forest Regression
   └── many more
```

---

## Confusion 3: Why does the model make mistakes?

Because real-world data is noisy.

Example:

Two campaigns can have the same budget but different conversions because of:

```text
audience quality
landing page
brand awareness
seasonality
competitor activity
ad copy
product price
```

So ML tries to find the best general pattern, not a perfect rule.

---

## Confusion 4: What does the model learn?

In simple linear regression, it learns:

```text
w and b
```

Meaning:

```text
how strongly inputs affect the output
```

In more advanced ML, it learns many parameters.

---

## Confusion 5: Why do we need loss?

Because the model needs feedback.

Loss tells the model:

```text
Your prediction is wrong by this much.
```

Then the model improves.

---

# 23. Practice Questions

## Question 1

You predict whether a lead will convert or not.

Answer:

```text
Classification
```

Why?

```text
The output is Yes / No.
```

---

## Question 2

You predict how many conversions a campaign will generate.

Answer:

```text
Regression
```

Why?

```text
The output is a number.
```

---

## Question 3

You predict whether a product is fast-moving, slow-moving, or dead stock.

Answer:

```text
Classification
```

Why?

```text
The output is a category.
```

---

## Question 4

You predict next month’s demand quantity.

Answer:

```text
Regression
```

Why?

```text
The output is a number.
```

---

## Question 5

Given:

| Hours | Points |
| ----: | -----: |
|     1 |      2 |
|     2 |      4 |
|     3 |      6 |
|     4 |      ? |

Prediction:

```text
8
```

Why?

```text
Points = Hours × 2
4 × 2 = 8
```

---

## Question 6

The model predicted 35 conversions.
Actual conversions were 40.

Error:

```text
5 conversions
```

---

## Question 7

The model has high loss.

Is it good or bad?

```text
Bad
```

Why?

```text
High loss means the model is making large mistakes.
```

---

# 24. Interview Explanation — Simple Version

You can say:

> Machine Learning means using historical data to learn patterns and make predictions on new data. In supervised learning, the model learns from examples where the correct answer is already known. If the answer is a category, such as yes/no, it is classification. If the answer is a number, such as revenue or conversions, it is regression. Linear regression is a regression method that finds the best straight-line relationship between input features and a numeric target.

---

# 25. Interview Explanation — Your Profile Version

You can say:

> In my digital marketing and BI work, I can apply supervised learning to campaign and customer data. For example, I can use features like impressions, clicks, CPC, device, country, and budget to predict conversions. If I predict whether a lead will convert, that is classification. If I predict the number of conversions or revenue, that is regression. Linear regression can be used as a simple baseline model to understand numeric relationships such as ad spend versus conversions.

---

# 26. CV-Relevant ML Project Ideas

## Project 1: Campaign Conversion Prediction

```text
Goal: Predict number of conversions
Type: Regression
Features: impressions, clicks, CTR, CPC, budget, device, country
Label: conversions
Business value: better budget planning
```

CV bullet:

```text
Built a regression model using historical campaign data to predict conversions and support digital marketing budget optimization.
```

---

## Project 2: Lead Conversion Classification

```text
Goal: Predict whether a lead will convert
Type: Classification
Features: source, device, session duration, pages visited, campaign, country
Label: converted yes/no
Business value: prioritize high-quality leads
```

CV bullet:

```text
Developed a classification model to predict lead conversion probability and identify high-value traffic segments.
```

---

## Project 3: Inventory Demand Forecasting

```text
Goal: Predict future product demand
Type: Regression
Features: sales history, stock level, season, category, lead time
Label: future demand
Business value: reduce overstock and stockouts
```

CV bullet:

```text
Created a demand prediction model using historical sales and inventory data to improve stock planning and reduce inventory risk.
```

---

## Project 4: Slow-Moving Product Classification

```text
Goal: Classify product movement
Type: Classification
Features: sales velocity, stock age, stock quantity, category, margin
Label: fast-moving / slow-moving / dead stock
Business value: inventory optimization
```

CV bullet:

```text
Built a classification model to identify slow-moving inventory and support data-driven stock optimization.
```

---

# 27. Final Memory Version

Memorize this:

```text
ML = learn from old data → predict new data

Features = input columns
Label = answer column

Supervised learning = data has correct answers

Classification = predict category
Regression = predict number
Linear regression = regression using a straight line

Prediction = model answer
Actual = real answer
Error = difference
Loss = overall mistake
MSE = average squared mistake
Gradient descent = step-by-step method to reduce loss
Learning rate = size of each learning step
```

---

# 28. The Most Important Beginner Test

Whenever you see an ML problem, ask this:

```text
What am I trying to predict?
```

Then ask:

```text
Is the answer a category or a number?
```

If category:

```text
Classification
```

If number:

```text
Regression
```

If number and the relationship is a straight-line pattern:

```text
Linear Regression
```

---

# 29. One Final Visual Summary

```text
                           Machine Learning
                                  |
                                  v
                         Supervised Learning
                    Data has inputs and answers
                                  |
             +--------------------+--------------------+
             |                                         |
             v                                         v
      Classification                              Regression
   Predict category/class                     Predict number/value
             |                                         |
             |                                         v
             |                                Linear Regression
             |                         Predict number using a line
             |
 Examples:                                  Examples:
 Yes/No lead conversion                     number of conversions
 Good/Bad campaign                          future demand
 Fast/Slow product                          revenue forecast
 Cat/Dog image                              house price
```

---

# 30. Your Direction

For your career profile, focus most on these ML applications:

## Digital Marketing

```text
Classification:
- lead conversion yes/no
- high-quality vs low-quality traffic
- campaign profitable or not

Regression:
- conversions prediction
- revenue prediction
- CPC / CPA forecasting
- ROAS forecasting
```

## Inventory / BI

```text
Classification:
- fast-moving vs slow-moving products
- stockout risk high/low
- supplier risk category

Regression:
- demand forecasting
- sales quantity prediction
- inventory requirement prediction
- revenue forecasting
```

## Dashboard Integration

ML results can become BI dashboard KPIs:

```text
Predicted conversions
Conversion probability
Forecasted demand
Stockout risk score
Slow-moving inventory category
Forecast vs actual error
```

This is how ML becomes useful for your CV, interviews, and real Data Analyst / BI work.
