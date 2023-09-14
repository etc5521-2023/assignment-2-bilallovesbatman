# Q1

## Part E

- Me: What do i talk about for a density plot? Currently I have mentioned the modality of the plot and the talked about the spread

AI: When discussing a density plot, you can cover several aspects to provide a comprehensive description and interpretation:

Modality: As you've mentioned, start by identifying the modality of the plot. This refers to the number of peaks or modes in the distribution. Is it unimodal (one peak), bimodal (two peaks), trimodal (three peaks), or multimodal (more than three peaks)? Describe the modality and its significance if relevant to your analysis.

Spread/Dispersion: Discuss the spread or dispersion of the data. Are the data points tightly clustered around the peak(s), or is there significant variability? You can mention the concept of standard deviation or interquartile range to quantify the spread.

Skewness: Determine whether the distribution is skewed or symmetrical. Skewness refers to the asymmetry in the distribution. Is it positively skewed (long tail on the right), negatively skewed (long tail on the left), or approximately symmetrical?

Central Tendency: Mention the central tendency of the data. What is the central value or values around which the data is concentrated? Discuss the mean, median, or mode, depending on the distribution's characteristics.

Outliers: Identify any outliers if present. Outliers are data points that significantly deviate from the main body of the distribution. Discuss their potential impact on the interpretation of the data.

Density Peaks: Describe the locations and heights of density peaks. What do these peaks represent in the context of your data analysis?

Axis Labels and Scaling: Mention the scales of the x-axis and y-axis. Are they linear or log-scaled? Ensure you've labeled your axes correctly to provide context to the reader.

Interpretation: Explain what the distribution represents in the context of your analysis.

Comparison: If relevant, compare this density plot to other density plots or distributions. Are there significant differences or similarities between them?

Conclusion: Summarize your findings from the density plot. What insights or patterns have you discovered? How do these findings contribute to your overall analysis or research objectives?

Remember to use descriptive language, visual cues, and statistics (if applicable) to support your discussion. Interpretation may vary depending on the specific characteristics of your data and the goals of your analysis.

--------

ANALYSIS: ChatGPT helped me to interpret the density plot. 

# Q2

## Part E

ME: I have used the following code to create a scatterplot for average rating of genres vs their votes:


```{r}
ggplot(movies_2023, aes(
  x = averageRating,
  y = numVotes
)) +
  geom_point(color = "purple") +
  scale_x_continuous(breaks = c(0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10)) +
  theme_classic()
```

On the y axis, I am getting votes in the form of, for example, 1e+05. I want to show complete numbers

AI: To display the numbers on the y-axis as complete numbers rather than in scientific notation (e.g., 1e+05), you can use the scale_y_continuous() function with the labels argument to format the axis labels. You can use the scales package to help format the numbers. Here's how you can modify your code to achieve this:

library(scales)  # Load the scales package

ggplot(movies_2023, aes(
  x = averageRating,
  y = numVotes
)) +
  geom_point(color = "purple") +
  scale_x_continuous(breaks = c(0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10)) +
  scale_y_continuous(labels = comma, breaks = scales::pretty_breaks()) +  # Use 'comma' to format labels
  theme_classic()

In this code, we use the comma function from the scales package to format the labels on the y-axis with commas to make them more readable. The scales::pretty_breaks() function is used to set suitable breaks on the y-axis. This should display the y-axis labels as complete numbers.

ME: It says object comma not found

AI: I apologize for the confusion. It seems that the comma function from the scales package is not recognized. You can achieve the same result by using the scales::comma_format() function. Here's the modified code:

ggplot(movies_2023, aes(
  x = averageRating,
  y = numVotes
)) +
  geom_point(color = "purple") +
  scale_x_continuous(breaks = c(0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10)) +
  scale_y_continuous(labels = scales::comma_format(), breaks = scales::pretty_breaks()) +
  theme_classic()

This should format the y-axis labels with commas, displaying the numbers as complete integers.

--------

ANALYSIS: ChatGPT helped me to fix the y-axis scale.

## Part F

Me: I have the following plots and I wish to show them together:

f_scatter <- ggplot(movies_2023, aes(
  x = averageRating,
  y = as.numeric(runtimeMinutes)
)) +
  geom_point(color = "purple") +
  geom_smooth(method = "lm") +
  labs(x = "Average Rating",
       y = "Runtime (minutes)") +
  ggtitle("Scatter: Movie Runtime vs Movie Ratings") +
   scale_x_continuous(breaks = c(0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10)) +
  theme_classic()

ratings_bin <- c(0, 2, 4, 6, 8, 10)

f_boxplot <- ggplot(movies_2023, aes(
  x = cut(averageRating, breaks = ratings_bin),
  y = as.numeric(runtimeMinutes)
)) +
  geom_boxplot(fill = "steelblue") +
  labs(x = "Average Ratings",
       y = "Runtime (minutes)") +
  ggtitle("Boxplot: Movie Runtime vs Movie Ratings") +
  theme_classic()

f_violin <- ggplot(movies_2023, aes(
  x = cut(averageRating, breaks = ratings_bin),
  y = as.numeric(runtimeMinutes)
)) +
  geom_violin(fill = "darkgreen") +
  labs(x = "Average Ratings",
       y = "Runtime (minutes)") +
  ggtitle("Violin: Movie Runtime vs Movie Ratings") +
  theme_classic()
  
AI: To display these plots together, you can arrange them using the grid.arrange function from the gridExtra package. Here's how you can do it:

First, make sure you have the gridExtra package installed. If you don't have it, you can install it using:

install.packages("gridExtra")

Now, you can arrange your plots as follows:

library(gridExtra)

# Arrange the plots
grid.arrange(f_scatter, f_boxplot, f_violin, ncol = 2)

# You can customize the layout further if needed, e.g., adjust heights and widths.

This code will arrange the scatter, boxplot, and violin plots side by side in two columns. You can adjust the ncol parameter to change the number of columns in the arrangement.

Make sure to execute the code after loading the necessary libraries and creating your plots.


--------

ANALYSIS: ChatGPT helped me to arrange 3 plots together.

# Q3

## Part d

ME: 
```
ggplot(tb_aus_neighb, aes(
  x = year,
  y = total_detected,
  color = country
)) +
  geom_line()
```
I want my y axis to show as complete numbers, not 3e +05

AI: If you want to display the y-axis labels as complete numbers (without scientific notation) in your ggplot, you can use the scale_y_continuous function and specify the labels argument to format the labels as integers. Here's how you can modify your ggplot code:

```
library(ggplot2)

ggplot(tb_aus_neighb, aes(
  x = year,
  y = total_detected,
  color = country
)) +
  geom_line() +
  scale_y_continuous(labels = scales::comma)  # Use comma formatting for labels

```

In this code, we use scale_y_continuous and scales::comma to format the y-axis labels as complete numbers with commas for better readability. This will display the y-axis labels in standard integer format rather than in scientific notation.

-------

ANALYSIS: ChatGPT helped me to display y axis in standard form.

## Part e

ME: How do i use a previous value from a data? For example, to perform percentage change

AI: To use a previous value from a data frame column or vector in R, you can utilize the lag function from the dplyr package, which allows you to access the previous value of a variable. You can then use this previous value to perform calculations like calculating percentage changes between consecutive values.

Here's how you can use lag to calculate percentage changes in a data frame:

```
library(dplyr)

# Sample data frame with a variable 'value' representing the values over time
df <- data.frame(year = 1:5, value = c(10, 15, 20, 25, 30))

# Calculate percentage change using lag
df <- df %>%
  mutate(prev_value = lag(value),  # Create a new column for the previous value
         percentage_change = (value - prev_value) / prev_value * 100)

# View the resulting data frame
print(df)
```

In this code:

We create a sample data frame named df with a variable value representing values over time.

We use mutate to create a new column named prev_value where we store the previous value of value using lag.

We calculate the percentage change by subtracting the previous value from the current value, dividing by the previous value, and then multiplying by 100 to get the percentage change.

By using lag in this way, you can access the previous value and perform various calculations, including percentage changes, differences, or any other operations that involve comparing current values with their previous counterparts.

-------

ANALYSIS: ChatGPT helped me to calculate percentage change in R effeciently.
